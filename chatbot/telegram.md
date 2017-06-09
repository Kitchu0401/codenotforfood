# 왜 Telegram 챗봇인가?

Telegram(이하 텔레그램) 챗봇을 활용하여 *모임문화 플랫폼 온오프믹스*의 이벤트 알리미 구축을 시작한지도 일주일이 되어간다.

아직 편의성을 고려한 많은 기능들이 todo list로 남은 상태지만, 개략적인 뼈대를 잡은 시점에서 챗봇 구현에 대한 경험담을 조금씩 정리 해보려고 한다.

먼저 _왜_ 텔레그램을 선택했는가?

최초 챗봇을 만들고자 했을 때 후보로 생각했던 플랫은 두 가지, 카카오톡과 디스코드였다.



# WebHook 설정

두 가지 방법이 있음.

1. https 서버로 직접 웹훅을 push 받는 방법

    인증서 blar blar - 이런건 알아서 하시고

    self-signed 인증서라는게 있음.

      ``` sh
      curl -F "url=https://kitchu.lazecrew.com:8443/event/webhook" -F "certificate=@telegram-self-signed-cert.pem" https://api.telegram.org/bot393049254:AAFNqTD164CqYsJfRBwzU4aeF2hfOKRenwo/setWebhook
      ```

    이렇게 해두고 해당 서버로 요청받아 직접 처리 할 것.

      ``` js
      var https = require('https')
      var express = require('express')
      var fs = require('fs')
      var morgan = require('morgan')
      var bodyParser = require('body-parser')
      var TelegramBot = require('node-telegram-bot-api')

      var telegramBotToken = '393049254:AAFNqTD164CqYsJfRBwzU4aeF2hfOKRenwo'

      var bot = new TelegramBot(telegramBotToken)
      var options = {
        key: fs.readFileSync('./telegram-self-signed-cert.key'),
        cert: fs.readFileSync('./telegram-self-signed-cert.pem')
      }

      var port = 443
      var app = express()
      app.use(morgan('dev'))
      app.use(bodyParser.json())
      app.use(bodyParser.urlencoded({ extended: false }))

      app.post('/event/webhook', function (req, res, next) {
        var message = req.body.message
        bot.sendMessage(message.chat.id, 'Recieved: ' + message.text)
        res.sendStatus(200)
      })

      https.createServer(options, app).listen(port, function () {
        console.log('https server listening on port: ', port)
      })
      ```
