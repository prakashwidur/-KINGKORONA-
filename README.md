# -KINGKORONA-
<h6>🤺KING KORONA🤺🔥</h6>
<div align="center">		
<img src= "https://camo.githubusercontent.com/71b837571c48af3aa60a73dbc9d5936aa359d78efbfa8a6743cbbbc16b80ef4d/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f3830353930323039333930363630383138362f3830353931333937323533353539303932322f74656e6f722e676966"/>
</p>
<div align="center">
<div align="center">		
<img src= "https://te.legra.ph/file/8b3968006c324b90b9ae4.jpg"/>
</p>
<div align="center">
<div align="center">		
<img src= "https://camo.githubusercontent.com/71b837571c48af3aa60a73dbc9d5936aa359d78efbfa8a6743cbbbc16b80ef4d/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f3830353930323039333930363630383138362f3830353931333937323533353539303932322f74656e6f722e676966"/>
</p>
<div align="center">
<h2>KING RAWANA V2 WHATSAPP USER BOT🔥</h2>


import makeWASocket, { DisconnectReason } from '@adiwajshing/baileys'
import { Boom } from '@hapi/boom'

async function connectToWhatsApp () {
    const sock = makeWASocket({
        // can provide additional config here
        printQRInTerminal: true
    })
    sock.ev.on('connection.update', (update) => {
        const { connection, lastDisconnect } = update
        if(connection === 'close') {
            const shouldReconnect = (lastDisconnect.error as Boom)?.output?.statusCode !== DisconnectReason.loggedOut
            console.log('connection closed due to ', lastDisconnect.error, ', reconnecting ', shouldReconnect)
            // reconnect if not logged out
            if(shouldReconnect) {
                connectToWhatsApp()
            }
        } else if(connection === 'open') {
            console.log('opened connection')
        }
    })
    sock.ev.on('messages.upsert', m => {
        console.log(JSON.stringify(m, undefined, 2))

        console.log('replying to', m.messages[0].key.remoteJid)
        await sock.sendMessage(m.messages[0].key.remoteJid!, { text: 'Hello there!' })
    })
}
// run in main file
connectToWhatsApp()
