# Buf Tours and Tutorials

This repository contains all of the example code for the Buf tours and tutorials:

- **[Buf CLI tour][buf-cli]** – Introduces you to key features of the Buf CLI, including generating code, detecting
  breaking changes, and linting and formatting your Protobuf files.

- **[Buf Schema Registry (BSR) tour][bsr]** – Introduces you to key features of the BSR, including creating and
  publishing modules, managing dependencies, and using generated SDKs.

- **[Breaking change detection tutorial][breaking]** – Walks you through common use cases for local breaking change
  detection.

- **[Code linting tutorial][lint]** – Demonstrates how the Buf CLI code linter can help ensure forward compatibility
  in your Protobuf files.

[breaking]: https://buf.build/docs/breaking/tutorial
[bsr]: https://buf.build/docs/tutorials/getting-started-with-bsr
[buf-cli]: https://buf.build/docs/tutorials/getting-started-with-buf-cli
[lint]: https://buf.build/docs/lint/tutorial

## buf 
- Linting : コードの整形


- breaking changes:  APIのバージョンアップ時に互換性の維持をおこなう



- code generation:  プロトコルバッファーから各種プログラミング言語用のコードの自動生成



- schema manegement:  データベースやデータフォーマットにおいて、その構造を定義を効率的に管理



 ## 設定とビルド
 protoファイルで buf.yamlの設定を行う
  ```sh
buf mod init
buf build
echo $?
```

## コードの生成
getting-started-with-buf-cli で行う
```sh
touch buf.gen.yaml
```
buf.gen.yamlに Goと Connect-Goのプラグインを含める

connectスタブの生成
```sh
buf generate proto
```

## API lint
```sh
buf lint proto
```

## lint エラーの無視の設定を追加する

```sh
# google/type/datetime.proto
+  ignore:
+    - google/type/datetime.proto
```

## コード変更の追跡
```sh
buf breaking proto --against "../../.git#subdir=start/getting-started-with-buf-cli/proto"
```


- サーバの立て方
```sh
cd finish/getting-started-with-buf-cli
go mod tidy
go run server/main.go
```

- リクエスト
```sh
buf curl \
  --schema proto \
  --data '{"pet_type": "PET_TYPE_SNAKE", "name": "Ekans"}' \
  http://localhost:8080/pet.v1.PetStoreService/PutPet
```


