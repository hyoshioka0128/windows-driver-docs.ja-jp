---
title: NDKPI 関数の実装
description: NDK 対応のミニポート ドライバーでは、すべて NDK_FN_XXX コールバック関数のエントリ ポイントを登録する必要があります。 NDKPI プロバイダーのコールバック関数のすべてが必須です。[なし] は省略可能です。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfdd195d03f2a5576b140f56b5eb08cda2b4581
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529625"
---
# <a name="implementing-ndkpi-functions"></a>NDKPI 関数の実装


NDK 対応のミニポート ドライバーは、すべてのエントリ ポイントを登録する必要があります[NDK\_FN\_*XXX*コールバック関数](https://msdn.microsoft.com/library/windows/hardware/jj206453)します。 NDKPI プロバイダーのコールバック関数のすべてが必須です。[なし] は省略可能です。

これらの関数のサポートを登録するには、ミニポート ドライバーでは、「オブジェクトのディスパッチ テーブル」のデータ構造で、エントリ ポイントを格納、次の表の列。

| オブジェクトの種類                                               | この関数によって作成されました。                                                                                                       | オブジェクトのディスパッチ テーブル                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK\_ADAPTER**](https://msdn.microsoft.com/library/windows/hardware/hh439848)                  | [*OPEN\_NDK\_ADAPTER\_HANDLER*](https://msdn.microsoft.com/library/windows/hardware/hh440105)                                                             | [**NDK\_ADAPTER\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439850)                  |
| [**NDK\_CONNECTOR**](https://msdn.microsoft.com/library/windows/hardware/hh439852)              | [*NDK\_FN\_CREATE\_CONNECTOR*](https://msdn.microsoft.com/library/windows/hardware/hh439872)                                                               | [**NDK\_コネクタ\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/hh439853)              |
| [**NDK\_CQ**](https://msdn.microsoft.com/library/windows/hardware/hh439854)                            | [*NDK\_FN\_CREATE\_CQ*](https://msdn.microsoft.com/library/windows/hardware/hh439873)                                                                             | [**NDK\_CQ\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439855)                            |
| [**NDK\_LISTENER**](https://msdn.microsoft.com/library/windows/hardware/hh439918)                | [*NDK\_FN\_CREATE\_LISTENER*](https://msdn.microsoft.com/library/windows/hardware/hh439874)                                                                 | [**NDK\_リスナー\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/hh439919)                |
| [**NDK\_MR**](https://msdn.microsoft.com/library/windows/hardware/hh439922)                            | [*NDK\_FN\_CREATE\_MR*](https://msdn.microsoft.com/library/windows/hardware/hh439875)                                                                             | [**NDK\_MR\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/hh439924)                            |
| [**NDK\_MW**](https://msdn.microsoft.com/library/windows/hardware/hh439926)                            | [*NDK\_FN\_CREATE\_MW*](https://msdn.microsoft.com/library/windows/hardware/hh439876)                                                                             | [**NDK\_MW\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/hh439927)                            |
| [**NDK\_PD**](https://msdn.microsoft.com/library/windows/hardware/hh439931)                            | [*NDK\_FN\_CREATE\_PD*](https://msdn.microsoft.com/library/windows/hardware/hh439877)                                                                             | [**NDK\_PD\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/hh439932)                            |
| [**NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)                            | [*NDK\_FN\_作成\_QP* ](https://msdn.microsoft.com/library/windows/hardware/hh439878)または[ *NDK\_FN\_作成\_QP\_WITH\_手順*](https://msdn.microsoft.com/library/windows/hardware/hh439880)   | [**NDK\_QP\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439934)                            |
| [**NDK\_SHARED\_エンドポイント**](https://msdn.microsoft.com/library/windows/hardware/hh439937) | [*NDK\_FN\_作成\_SHARED\_エンドポイント*](https://msdn.microsoft.com/library/windows/hardware/hh439882)                                                  | [**NDK\_SHARED\_エンドポイント\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/hh439938) |
| [**NDK\_SRQ**](https://msdn.microsoft.com/library/windows/hardware/hh439939)                          | [*NDK\_FN\_作成\_の*](https://msdn.microsoft.com/library/windows/hardware/hh439883)または[ *NDK\_FN\_作成\_QP\_WITH\_手順*](https://msdn.microsoft.com/library/windows/hardware/hh439880) | [**NDK\_SRQ\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439940)                          |

 

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






