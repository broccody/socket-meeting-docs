# Socket Meeting Document(v1)

## Actions

##### 1. startCall
start video call (1-1) and wait util callee accept calling
```javascript
const message = {
    id: "startCall",
    project: "project",
    robotId: "1",   // target robot id
    videoId: "0",   // (optional) default '0'
    roomId: "room-id"   // (optional) for custom room id
}
socket.emit("meeting", message)
```

##### 2. startGroupCall
start video group call and wait util someone join room

```javascript
const message = {
    id: "startGroupCall",
    project: "room-project",
    roomId: "room-id",   // (optional) for custom room id
    roomName: "room-name",   // (optional) for custom room name
}
socket.emit("meeting", message)
```

##### 3. startMeeting
start meeting (no waiting)
```javascript
const message = {
    id: "startMeeting",
    project: "room-project",
    roomId: "room-id",   // (optional) for custom room id
    roomName: "room-name",   // (optional) for custom room name
}
socket.emit("meeting", message)
```

##### 4. joinRoom
join meeting room
```javascript
const message = {
    id: "joinRoom",
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 5. leaveRoom
leave meeting room
```javascript
const message = {
    id: "leaveRoom",
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 6. rejoinRoom
join meeting re-room
```javascript
const message = {
    id: "rejoinRoom",
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 7. acceptCall
accept incoming call
```javascript
const message = {
    id: "acceptCall",
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 8. rejectCall
reject incoming call
```javascript
const message = {
    id: "rejectCall",
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 9. cancelCall
cancel (1-1) calling (from caller)
```javascript
const message = {
    id: "cancelCall",
    robotId: "callee-robot-id"
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 10. cancelGroupCall
cancel group calling (from caller)
```javascript
const message = {
    id: "cancelGroupCall",
    roomId: "room-id",
    project: "room-project"
}
socket.emit("meeting", message)
```

##### 11. invite
invite other to join room
```javascript
const message = {
    id: "invite",
    robotId: "receiver-robot-id",
    videoId: "receiver-video-id"    // (optional)
    roomId: "room-id",
    project: "room-project"
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
        roomId: "room-id"
        roomName: "room-name",
        roomType: "room-type"
        project: "room-project",
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

##### rejoinRoomSuccess
event on join re-room success

```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on rejoinRoomSuccess
    {
        id: "rejoinRoomSuccess",
        roomId: "room-id"
        roomName: "room-name",
        roomType: "room-type"
        project: "room-project",
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
        roomId: "room-id"
        roomName: "room-name",
        roomType: "room-type"
        project: "room-project",
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

##### userAcceptCall
event on user (callee) accept calling
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on userAcceptCall
    {
        id: 'userAcceptCall',
        fromSocket: "sender-socker-id",
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
        fromSocket: "sender-socker-id",
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

##### userCancelCall
event on user (caller) cancel calling
```javascript
socket.on("meeting", msg => {
    console.log(msg)
/*  msg on userCancelCall
    {
        id: 'userCancelCall',
        fromSocket: "sender-socker-id",
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
        fromSocket: "sender-socker-id",
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
        fromSocket: "sender-socker-id",
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

