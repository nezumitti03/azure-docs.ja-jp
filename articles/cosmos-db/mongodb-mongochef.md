---
title: Studio 3T を使用して Azure Cosmos DB の MongoDB 用 API に接続する
description: Studio 3T を使用して Azure Cosmos DB の MongoDB 用 API に接続する方法について説明します。
ms.service: cosmos-db
ms.subservice: cosmosdb-mongo
ms.topic: conceptual
ms.date: 03/20/2020
author: timsander1
ms.author: tisande
ms.custom: seodec18
ms.openlocfilehash: 84b703cceeb130b177b8ab32281ef616b1ec632b
ms.sourcegitcommit: 980c3d827cc0f25b94b1eb93fd3d9041f3593036
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2020
ms.locfileid: "80548837"
---
# <a name="connect-to-an-azure-cosmos-account-using-studio-3t"></a>Studio 3T を使用して Azure Cosmos アカウントに接続する

Studio 3T を使用して Azure Cosmos DB の MongoDB 用 API に接続するには、次のことを行う必要があります。

* [Studio 3T](https://studio3t.com/) をダウンロードしてインストールします。
* Azure Cosmos アカウントの[接続文字列](connect-mongodb-account.md)情報を取得します。

## <a name="create-the-connection-in-studio-3t"></a>Studio 3T で接続を作成する

Studio 3T 接続マネージャーに Azure Cosmos アカウントを追加するには、次の手順を行います。

1. 「[Azure Cosmos DB への MongoDB アプリケーションの接続](connect-mongodb-account.md)」の記事にある手順を使用して、Azure Cosmos DB の MongoDB 用 API アカウントの接続情報を取得します。

    ![接続文字列のページのスクリーンショット](./media/mongodb-mongochef/ConnectionStringBlade.png)

2. **[Connect (接続)]** をクリックして接続マネージャーを開き、 **[New Connection (新しい接続)]** をクリックします。

    ![Studio 3T 接続マネージャーのスクリーンショット](./media/mongodb-mongochef/ConnectionManager.png)
3. **[新しい接続]** ウィンドウの **[サーバー]** タブで、Azure Cosmos アカウントのホスト (FQDN) とポートを入力します。

    ![Studio 3T 接続マネージャーの [Server]\(サーバー\) タブのスクリーンショット](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. **[New Connection]\(新しい接続)** ウィンドウの **[認証]** タブで、 **[Basic (MONGODB-CR or SCARM-SHA-1)] (基本 (MONGODB-CR または SCARM-SHA-1))** の認証モードを選択し、ユーザー名とパスワードを入力します。  既定の認証データベース (admin) をそのまま使用するか、または独自の値を指定します。

    ![Studio 3T 接続マネージャーの [Authentication]\(認証\) タブのスクリーンショット](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. **[New Connection (新しい接続)]** ウィンドウの **[SSL]** タブで、 **[Use SSL protocol to connect (SSL プロトコルを使用して接続する)]** チェック ボックスをオンにし、 **[Accept server self-signed SSL certificates (サーバー自己署名 SSL 証明書を受け付ける)]** オプション ボタンをオンにします。

    ![Studio 3T 接続マネージャーの [SSL] タブのスクリーンショット](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. **[Test Connection (接続のテスト)]** をクリックして接続情報を検証し、 **[OK]** をクリックして [New Connection (新しい接続)] ウィンドウに戻り、 **[Save (保存)]** をクリックします。

    ![Studio 3T のテスト接続ウィンドウのスクリーンショット](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-studio-3t-to-create-a-database-collection-and-documents"></a>Studio 3T を使用してデータベース、コレクション、およびドキュメントを作成する
Studio 3T を使用してデータベース、コレクション、およびドキュメントを作成するには、次の手順を実行します。

1. **接続マネージャー**で目的の接続を強調表示し、 **[Connect (接続)]** をクリックします。

    ![Studio 3T 接続マネージャーのスクリーンショット](./media/mongodb-mongochef/ConnectToAccount.png)
2. ホストを右クリックし、 **[データベースの追加]** を選択します。  データベースの名前を指定し、 **[OK]** をクリックします。

    ![Studio 3T の [Add Database]\(データベースの追加\) オプションのスクリーンショット](./media/mongodb-mongochef/AddDatabase1.png)
3. データベースを右クリックし、 **[コレクションの追加]** を選択します。  コレクションの名前を指定し、 **[Create (作成)]** をクリックします。

    ![Studio 3T の [Add Collection]\(コレクションの追加\) オプションのスクリーンショット](./media/mongodb-mongochef/AddCollection.png)
4. **[Collection (コレクション)]** メニュー項目をクリックし、 **[Add Document (ドキュメントの追加)]** をクリックします。

    ![Studio 3T の [Add Document]\(ドキュメントの追加\) オプションのスクリーンショット](./media/mongodb-mongochef/AddDocument1.png)
5. [Add Document (ドキュメントの追加)] ダイアログに次の情報を貼り付けて **[Add Document (ドキュメントの追加)]** をクリックします。

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. 今度は次の内容を含む別のドキュメントを追加します。

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. サンプル クエリを実行します。 たとえば姓が "Andersen" である世帯を検索し、parents フィールドと state フィールドを取得します。

    ![Mongo Chef のクエリ結果のスクリーンショット](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>次のステップ

- Azure Cosmos DB の MongoDB 用 API と共に [Robo 3T を使用する](mongodb-robomongo.md)方法を学びます。
- Azure Cosmos DB の MongoDB 用 API を使用した MongoDB の[サンプル](mongodb-samples.md)を調査します。
