---
title: 一个grpcServer实现多个proto文件
date: 2020-07-10 11:35:09
tags:
  - Golang
categories:
  - Golang
---

### 一个GRPCServer实现多个proto文件

1. 多个proto文件定义在同一个package包中
2. 每个proto文件中的service不相同（多个接口）
3. 注册GRPCServer的结构体需要实现多个proto文件中定义的接口的方法
4. 注册GRPCServer时需要调用每个pb.go文件中的RegisterXXXXServer方法

### 举例

- 第一个proto文件

  ```protobuf
  syntax = "proto3";
  
  package api;
  
  service Decision {
    rpc Decision(DecisionReq) returns (DecisionRes){}
  }
  
  message DecisionReq {
    string Headers = 1;
    int64 MemberId = 2;
  }
  
  message Error {
    string Error = 1;
    int64  Code = 2;
  }
  
  message DecisionRes {
    int64 Code = 1;
    Error Result = 2;
    int64  ResultType = 3;
    string RequestId = 4;
    int64 Timestamp = 5;
  }
  ```

- 第二个proto文件

  ```protobuf
  syntax = "proto3";
  
  package api;
  
  service Api {
    // Sends a greeting
    rpc HelloWorld(HelloReq) returns (HelloRes) {}
  }
  
  message HelloReq {
    string Name = 1;
  }
  
  message HelloRes {
    string Res = 1;
  }
  ```

- 注册server

  ```go
  package handler
  
  import (
  	pb "api_server/handler/proto"
  	"google.golang.org/grpc"
  	"log"
  	"net"
  )
  
  var gServer = grpc.NewServer()
  
  type Api struct{} // 实现多个proto文件中定义的方法
  
  func Start(addr string) {
  	conn, err := net.Listen("tcp", addr)
  	if err != nil {
  		log.Fatalf("net listen err: %v", err)
  	}
  	pb.RegisterApiServer(gServer, &Api{}) // 多次注册
  	pb.RegisterDecisionServer(gServer, &Api{}) // 多次注册
  	gErr := gServer.Serve(conn)
  	if gErr != nil {
  		log.Fatalf("grpc server err:%v", err)
  	}
  }
  
  func Stop() {
  	gServer.GracefulStop()
  	log.Println("grpc server stop")
  }
  ```

  