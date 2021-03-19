# Zoom-Clone

### Server
- Express
- Socket.io



### Client
- EJS

## Installation
- Install peer js
```
npm i -g peer
```
&

```sh
cd Zoom-Clone-master
peerjs --port 3001
npm run devStart
```
Using 3000 & 3001 port for server, peer server

## Connect
1. server 에서 '/' 에 접근하는 유저를 '/{uuid1}' 로 리다이렉트 시키고 이때 room.ejs 를 렌더링하면서 roomId 를 넘겨준다.
2. peer 서버에서 'open'에 바인딩된 socket이 join-room 이벤트를 roomId,userId와 emit 한다.
3. server 에 join-room 과 바인딩된 소켓은 roomId에 해당하는 방에 있는 유저들의 소켓에 'user-connected' 이벤트를 emit한다.
4. 새로 들어온 유저는 그 방에 자신의 스트림을 올리고 기존의 유저들은 새로 들어온 유저의 id를 받아 peers에 저장하고 자신의 스트림을 전송한다. (기존의 유저들은 브라우저에 자신의 스트림이 올라가있는 상태)
5. 새로 들어온 유저는 스트림들을 받아 video-grid에 화면들을 추가한다.

## Disconnect
1. 한 유저가 나가면 서버소켓은 해당 방의 유저들에게 "user-disconnected" 이벤트를 userId와 함께 emit 한다.
2. 그 방에 있던 유저들은 userId에 해당하는 video를 없애고 peers에서 close 한다.
