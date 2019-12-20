---
title: BCDEdit /ems
description: /Ems オプションは、指定されたオペレーティングシステムのブートエントリの緊急管理サービス (EMS) を有効または無効にします。
ms.assetid: 28a28fa9-e359-4fd7-be4d-9b4129db8ac7
ms.date: 05/21/2018
keywords:
- BCDEdit/ems ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /ems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6adc1e2cb94f1e2911f4c0df376459f9ec9c096a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209490"
---
<a name="bcdedit-ems"></a>BCDEdit /ems
============

**/Ems**オプションは、指定されたオペレーティングシステムのブートエントリの緊急管理サービス (ems) を有効または無効にします。

``` syntax
    bcdedit /ems [{ID}] { on | off } 

   
```

<a name="parameters"></a>パラメーター
----------

<strong>番号</strong>   

{**ID**} は、ブートエントリに関連付けられている GUID です。 {**ID**} を指定しない場合、コマンドは現在のオペレーティングシステムのブートエントリを変更します。 ブートエントリが指定されている場合は、ブートエントリに関連付けられている GUID を中かっこ {} で囲む必要があります。

### <a name="comments"></a>コメント

[**BCDEdit/emssettings**](bcdedit--emssettings.md)コマンドとそのパラメーターを使用して、すべてのブートエントリの EMS 設定を確立します。 次に、 **BCDEdit/ems**コマンドを使用して、特定のブートエントリの ems を有効にします。

EMS を使用すると、サーバーがネットワークに接続されていない場合や、他の標準のリモート管理ツールに接続されていない場合でも、ユーザーはサーバーの特定のコンポーネントをリモートで制御できます。 

### <a name="example"></a>例

次のコマンドでは、{49916baf05 e08-11db9af4000bdbd316a0} の id を持つブートエントリの EMS を有効にします。

```
bcdedit /ems {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

 

 





