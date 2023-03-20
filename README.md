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
