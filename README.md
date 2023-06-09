# grpc-sample

### 準備
+ brew install protobuf
+ go mod init mygrpc
+ go get -u google.golang.org/grpc
+ go get -u google.golang.org/grpc/cmd/protoc-gen-go-grpc
+ brew install grpcurl


### コード生成コマンド(.protoファイル配下で実行)
+ `protoc --go_out=../pkg/grpc --go_opt=paths=source_relative \
	--go-grpc_out=../pkg/grpc --go-grpc_opt=paths=source_relative \
	hello.proto`


### gcurl実行
```
$ grpcurl -plaintext -d '{"name": "hsaki"}' localhost:8080 myapp.GreetingService.Hello
{
  "message": "Hello, hsaki!"
}
```
```
$ grpcurl -plaintext -d '{"name": "hsaki"}' localhost:8080 myapp.GreetingService.HelloServerStream
{
  "message": "[0] Hello, hsaki!"
}
{
  "message": "[1] Hello, hsaki!"
}
{
  "message": "[2] Hello, hsaki!"
}
{
  "message": "[3] Hello, hsaki!"
}
{
  "message": "[4] Hello, hsaki!"
}
```

```
$ grpcurl -plaintext -d '{"name": "hsaki"}{"name": "a-san"}{"name": "b-san"}{"name": "c-san"}{"name": "d-san"}' localhost:8080 myapp.GreetingService.HelloClientStream
{
  "message": "Hello, [hsaki a-san b-san c-san d-san]!"
}
```

```
$ grpcurl -plaintext -d '{"name": "hsaki"}{"name": "a-san"}{"name": "b-san"}{"name": "c-san"}{"name": "d-san"}' localhost:8080 myapp.GreetingService.HelloBiStreams
{
  "message": "Hello, hsaki!"
}
{
  "message": "Hello, a-san!"
}
{
  "message": "Hello, b-san!"
}
{
  "message": "Hello, c-san!"
}
{
  "message": "Hello, d-san!"
}
```
