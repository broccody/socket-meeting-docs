# Socket Meeting Document

## Actions

##### 1. startCall
start video call (1-1) and wait util callee accept calling
```javascript
const message = {
    id: "startCall",
    robotId: "1",   // callee robot id
    videoId: "0",   // callee video id
    project: "DemoHospital>Depart1>Ward1"   // callee project
}
socket.emit("meeting", message)
```

##### 2. startMeeting
start video group
```javascript
const message = {
    id: "startMeeting",
    roomId: "meeting-01",
    roomName: "Regular Meeting",
    project: "DemoHospital>Depart1>Ward1"
}
socket.emit("meeting", message)
```

##### 3. joinRoom
join meeting room
```javascript
const message = {
    id: "joinRoom",
    roomId: "meeting-01",
    project: "DemoHospital>Depart1>Ward1"
}
socket.emit("meeting", message)
```

##### 4. leaveRoom
leave meeting room
```javascript
const message = {
    id: "leaveRoom",
    roomId: "meeting-01",
    project: "DemoHospital>Depart1>Ward1"
}
socket.emit("meeting", message)
```

##### 5. acceptCall
accept incoming call
```javascript
const message = {
    id: "acceptCall",
    to: "caller.id"
    roomId: "meeting-01",
    project: "DemoHospital>Depart1>Ward1"
}
socket.emit("meeting", message)
```

##### 7. invite
invite other to join room
```javascript
const message = {
    id: "invite",
    robotId: "receiver-robot-id",
    videoId: "receiver-video-id"
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 1. startCall
start video call (1-1) and wait util callee accept calling

```javascript
const message = {
    id: "startCall",
    robotId: "1",   // callee robot id
    videoId: "0",   // callee video id
    project: "DemoHospital>Depart1>Ward1"   // callee project
}
socket.emit("meeting", message)
```

## Events
##### joinRoomSuccess
event on join room success

```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on joinRoomSuccess
    {
        id: "joinRoomSuccess",
        roomId: "caller.id"
        roomName: "meeting-01",
        roomType: "meeting"
        project: "DemoHospital>Depart1>Ward1",
        members: [
            {
                id: "user-socket-id",
                robotId: "1",
                videoId: "0",
                name: "member 01",
                username: "member01"
            },
            {
                id: "user-socket-id",
                robotId: "2",
                videoId: "0",
                name: "member 02",
                username: "member02"
            }
        ]
    }
/*
})
```

##### joinRoomFailure
event on join room failure.

```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on joinRoomFailure
    {
        id: "joinRoomFailure",
        roomId: "meeting1"
        errorCode: 404
        errorMessage: "room not found"
    }
/*
})
```

##### userJoinRoom
event on user join room
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on userJoinRoom
    {
        id: "userJoinRoom",
        roomId: "caller.id"
        roomName: "meeting-01",
        roomType: "meeting"
        project: "DemoHospital>Depart1>Ward1",
        user: {
            id: "user-socket-id",
            robotId: "2",
            videoId: "0",
            name: "member 02",
            username: "member02"
        }
    }
/*
})
```

##### userLeaveRoom
event on user leave room
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on userLeaveRoom
    {
        id: "userLeaveRoom",
        roomId: "meeting1"
        roomName: "meeting-01",
        roomType: "meeting"
        project: "DemoHospital>Depart1>Ward1",
        user: {
            id: "user-socket-id",
            robotId: "2",
            videoId: "0",
            name: "member 02",
            username: "member02"
        }
    }
/*
})
```

##### closeRoom
event on room close
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on closeRoom
    {
        id: "closeRoom",
        roomId: "meeting1"
        roomName: "meeting-01",
        roomType: "meeting"
        project: "DemoHospital>Depart1>Ward1"
    }
/*
})
```

##### userAcceptCall
event on user (callee) accept calling
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on userAcceptCall
    {
        id: 'userAcceptCall',
        from: "sender-socker-id",
        fromName: "sender-name",
        fromRobotId: "sender-robot-id",
        fromUsername: "sender-username",
        roomId: "room-id",
        roomName: "room-name",
        roomType: "room-type",
        project: "room-project",
    }
/*
})
```

##### userRejectCall
event on user (callee) reject calling
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on userRejectCall
    {
        id: 'userRejectCall',
        from: "sender-socker-id",
        fromName: "sender-name",
        fromRobotId: "sender-robot-id",
        fromUsername: "sender-username",
        roomId: "room-id",
        roomName: "room-name",
        roomType: "room-type",
        project: "room-project",
    }
/*
})
```

##### incomingCall
event on receive incoming call
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on incomingCall
    {
        id: 'incomingCall',
        from: "sender-socker-id",
        fromName: "sender-name",
        fromRobotId: "sender-robot-id",
        fromUsername: "sender-username",
        roomId: "room-id",
        roomName: "room-name",
        roomType: "room-type",
        project: "room-project",
    }
/*
})
```

##### invite
event on receive invititaion
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on invite
    {
        id: 'invite',
        from: "sender-socker-id",
        fromName: "sender-name",
        fromRobotId: "sender-robot-id",
        fromUsername: "sender-username",
        roomId: "room-id",
        roomName: "room-name",
        roomType: "room-type",
        project: "room-project",
    }
/*
})
```

