---
title: OID_WDI_IHV_REQUEST
description: OID_WDI_IHV_REQUEST は IHV の機能拡張モジュールが、ミニポートに送信する情報を転送に使用されます。
ms.assetid: d5639def-ddde-4972-b331-46c0f768d155
ms.date: 07/18/2017
keywords:
- OID_WDI_IHV_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f43c8346914f3d22437ef37412f32ce862ac9eec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537081"
---
# <a name="oidwdiihvrequest"></a>OID\_WDI\_IHV\_要求


OID\_WDI\_IHV\_IHV の機能拡張モジュールが、ミニポートに送信する情報を転送するように要求を使用します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

このコマンドはすべてのタスクでシリアル化されません。 その他のプロパティと、タスクの M1、M3 をシリアル化されます。

## <a name="command-parameter"></a>コマンド パラメーター


| TLV                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                        |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------|
| [**WDI\_TLV\_IHV\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn926312) |                                | X        | IHV 機能拡張のモジュールからの情報。 |

 

## <a name="response-result"></a>応答の結果


| TLV                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                 |
|------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn926312) |                                | X        | IHV 機能拡張のモジュールに送信される応答です。 データ値として転送-IHV 機能拡張のモジュールには。 |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




