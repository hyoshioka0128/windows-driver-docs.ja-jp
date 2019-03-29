---
title: BCDEdit /ems
description: /Ems オプションを有効または指定したオペレーティング システムのブート エントリの緊急管理サービス (EMS) を無効にします。
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
ms.openlocfilehash: 5e405ee52ad1c34459f4099e894136454152459d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573933"
---
<a name="bcdedit-ems"></a>BCDEdit /ems
============

**/Ems**オプションを有効または指定したオペレーティング システムのブート エントリの緊急管理サービス (EMS) を無効にします。

``` syntax
    bcdedit /ems [{ID}] { on | off } 

   
```

<a name="parameters"></a>パラメーター
----------

<strong>{ID}</strong>   

{**ID**} ブート エントリに関連付けられた GUID です。 指定しない場合、{**ID**} のコマンドは、現在のオペレーティング システムのブート エントリを変更します。 ブート エントリが指定されている場合、ブート エントリに関連付けられている GUID が中かっこ {} で囲む必要があります。

### <a name="comments"></a>コメント

Windows Vista 以降では、使用[ **BCDEdit/emssettings** ](bcdedit--emssettings.md)コマンドとそのパラメーターは、すべてのブート エントリの EMS 設定を確立します。 次に、使用、 **BCDEdit/ems**コマンドを特定のブート エントリの EMS を有効にします。

EMS では、サーバーが、ネットワークまたはその他の標準のリモート管理ツールに接続されていない場合でも、サーバーの特定のコンポーネントをリモートで制御することができます。 EMS の詳細についてで緊急管理サービスの検索、 [Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=10111) web サイト。

### <a name="example"></a>例

次のコマンドは、{49916baf-0e08-11db-9af4-000bdbd316a0} の識別子を持つブート エントリの EMS を使用できます。

```
bcdedit /ems {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

 

 





