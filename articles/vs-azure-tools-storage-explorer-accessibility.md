---
title: Azure Storage Explorer のアクセシビリティ (プレビュー) | Microsoft Docs
description: Azure Storage Explorer のアクセシビリティ (プレビュー)
services: storage
documentationcenter: na
author: MrayermannMSFT
manager: jinglouMSFT
editor: ''
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/20/2018
ms.author: marayerm
ms.openlocfilehash: aa42d6b898a3cc474575f6c8dae65ff420fc8e30
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "60457268"
---
# <a name="storage-explorer-accessibility"></a>Storage Explorer のアクセシビリティ

## <a name="screen-readers"></a>スクリーン リーダー

Storage Explorer は、Windows と Mac でスクリーン リーダーの使用をサポートします。 各プラットフォームでは、次のスクリーン リーダーをお勧めします。

プラットフォーム | スクリーン リーダー
---------|--------------
Windows  | NVDA
Mac      | Voice Over
Linux    | (Linux ではスクリーン リーダーはサポートされません)

Storage Explorer の使用時にアクセシビリティの問題が発生した場合は、[GitHub に問題を開設](https://github.com/Microsoft/AzureStorageExplorer/issues)してください。

## <a name="zoom"></a>Zoom

Storage Explorer では、ズーム インによってテキストを拡大できます。 ズーム インするには、[ヘルプ] メニューの **[ズーム イン]** をクリックします。 [ヘルプ] メニューを使用して、ズーム アウトしたり、ズーム レベルを既定のレベルのリセットしたりすることもできます。

![[ヘルプ] メニューのズーム オプション][0]

ズーム設定によって、ほとんどの UI 要素のサイズが拡大されます。 また、すべての UI 要素が適切にスケーリングされるように、お使いの OS の大きなテキストおよび拡大/縮小設定を有効にすることを勧めします。

## <a name="high-contrast-themes"></a>ハイ コントラストのテーマ

Storage Explorer には、**ハイ コントラスト （淡色）** と**ハイ コントラスト (濃色)** という 2 つのハイ コントラスト テーマがあります。 テーマを変更するには、[ヘルプ] メニューの [テーマ] メニューから選択します。

![[テーマ] サブメニュー][1]

テーマの設定によって、ほとんどの UI 要素の色が変更されます。 また、すべての UI が適切に色付けされるように、お使いの OS に適合するハイ コントラストのテーマを有効にすることをお勧めします。

## <a name="shortcut-keys"></a>ショートカット キー

### <a name="window-commands"></a>ウィンドウ コマンド

command       | キーボード ショートカット
--------------|--------------------
新しいウィンドウ    | **Ctrl + Shift + N**
エディターを閉じる  | **Ctrl + F4**
終了する          | **Ctrl + Shift + W**

### <a name="navigation-commands"></a>ナビゲーション コマンド

command                | キーボード ショートカット
-----------------------|----------------------
次のパネルにフォーカス       | **F6**
前のグループにフォーカス   | **Shift + F6**
エクスプローラー               | **Ctrl + Shift + E**
アカウント管理     | **Ctrl + Shift + A**
サイドバーの切り替え        | **Ctrl + B**
アクティビティ ログ           | **Ctrl + Shift + L**
アクションとプロパティ | **Ctrl + Shift + P**
現在のエディター         | **Ctrl + Home**
次のエディター            | **Ctrl + PageDown**
前のエディター        | **Ctrl + PageUp**

### <a name="zoom-commands"></a>ズーム コマンド

command  | キーボード ショートカット
---------|------------------
拡大  | **Ctrl + =**
縮小 | **Ctrl + -**

### <a name="blob-and-file-share-editor-commands"></a>BLOB およびファイル共有エディター コマンド

command | キーボード ショートカット
--------|--------------------
戻る    | **Alt + ←**
転送 | **Alt + →**
上へ      | **Alt + ↑**

### <a name="editor-commands"></a>エディターのコマンド

command | キーボード ショートカット
--------|------------------
コピー    | **Ctrl + C**
切り取り     | **Ctrl + X**
貼り付け   | **Ctrl + V**
更新  | **Ctrl + R**

### <a name="other-commands"></a>その他のコマンド

command                | キーボード ショートカット
-----------------------|------------------
開発者ツールの切り替え | **F12**
再読み込み                 | **Alt + Control + R**

[0]: ./media/vs-azure-tools-storage-explorer-accessibility/Zoom.png
[1]: ./media/vs-azure-tools-storage-explorer-accessibility/HighContrast.png
