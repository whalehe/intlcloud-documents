## Overall Flowchart
![](https://main.qcloudimg.com/raw/b940c44c486d02f19c5a3fad3361b5f0.png)
## Integration Steps
### Step 1. Integrate the server with the gRPC framework
The game server communicates with GSE over gRPC. The gRPC framework can be integrated with the game server program in various programming languages to generate game server executable files. For more information on how to integrate GSE with the server in different languages, please see [gRPC - C++ Tutorial](https://intl.cloud.tencent.com/document/product/1055/37408), [gRPC - C# Tutorial](https://intl.cloud.tencent.com/document/product/1055/37409), [gRPC - Go Tutorial](https://intl.cloud.tencent.com/document/product/1055/37410), [gRPC - Java Tutorial](https://intl.cloud.tencent.com/document/product/1055/37411), [gRPC - Lua Tutorial](https://intl.cloud.tencent.com/document/product/1055/37412), and [gRPC - Node.js Tutorial](https://intl.cloud.tencent.com/document/product/1055/37413). For other languages, please see the [gRPC official documentation](http://doc.oschina.net/grpc).

### Step 2. Publish the program

1. Upload an asset package 
An asset package contains the executable files, dependency packages, and installation scripts of the game server. You need to package it as a zip package before uploading it. For more information, please see [Creating Asset Package](https://intl.cloud.tencent.com/document/product/1055/36674).
2. Create a server fleet 
Deploy the uploaded asset package on the created server fleet and complete process management, deployment configuration, scaling configuration, etc. For more information, please see [Creating Server Fleet](https://intl.cloud.tencent.com/document/product/1055/36675).   

### Step 3. Call a TencentCloud API to get the server address (IP:port or domain name)
You can get the server address (IP:port or domain name) by creating and placing a game server session.

#### Create a game server session
- Creation method:
  Create one by using a server fleet.
	Create one by using an alias.
- Call a TencentCloud API:
The client TencentCloud API call process varies by supporting mode of the game server session.
 * When a game server session only supports one game:
   - Create a game server session (CreateGameServerSession);
   - Join the game server session (JoinGameServerSession).
 * When a game server session supports multiple games or one service (such as login):
   - Query the game server session list (DescribeGameServerSessions) or search in the game server session list (SearchGameServerSessions);
   - If there is a game server session, join it (JoinGameServerSession);
   - If there is no game server session, create one (CreateGameServerSession) and join it (JoinGameServerSession).

 For more information on how to call TencentCloud APIs, please see [Creating Game Server Session](https://intl.cloud.tencent.com/document/product/1055/37416).

#### Place a game server session
- Creation method:
Create one by using a game server queue.

- Call a TencentCloud API:
 - Start placing a game server session (StartGameServerSessionPlacement);
 - Query the game server session placement (DescribeGameServerSessionPlacement);
 - Stop placing a game server session (StopGameServerSessionPlacement).

 For more information on how to call the TencentCloud APIs, please see [Placing Game Server Session](https://intl.cloud.tencent.com/document/product/1055/37417).

### Step 4. The client uses the IP:port or domain name to access the server
The client can connect to the target server through the `IP:port` or domain name returned in step 3.

## Workflow
![](https://main.qcloudimg.com/raw/02ec2067c8e06f5e1d1f3130aee7b81d.png)
