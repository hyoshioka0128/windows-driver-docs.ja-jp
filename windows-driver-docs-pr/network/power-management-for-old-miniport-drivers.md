---
title: 古いミニポート ドライバーの電源管理
description: 古いミニポート ドライバーの電源管理
ms.assetid: 676c8c4c-3fd7-4063-a704-2bbfdd03a94e
keywords:
- WDK の NDIS ミニポート、古いミニポート ドライバーの電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2aab7c0950cea4b5a90376f13365a5cc33b4aa1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530429"
---
# <a name="power-management-for-old-miniport-drivers"></a>古いミニポート ドライバーの電源管理





NDIS ミニポート ドライバーを古いミニポート ドライバーとして扱われますはいない電源管理に対応した場合。

-   初期化中に、バス ドライバーでは、こと、システムまたは NIC は電源管理に対応したことを示します。

-   ミニポート ドライバー返します NDIS\_状態\_への応答でサポートされていない、 [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)クエリ。 NDIS 5.1 以前のミニポート ドライバーや中間ドライバーは、この OID クエリを受信します。

-   ユーザーには、ユーザー インターフェイスでの電源管理が無効にします。

NDIS power manegement をサポートしない古いミニポート ドライバーの 2 つのデバイスの電源状態をサポートしています: highest-powered (D0) 状態と D3 の状態。

初期化中に、古いミニポート ドライバーは、NDIS がスリープ状態の (D3) 状態にシステム遷移する前にいない中止する必要がありますに指定できます。 により、このようなを示す値をするには、NDIS ミニポート ドライバー\_属性\_いいえ\_HALT\_ON\_で SUSPEND フラグ、 *AttributeFlags*パラメーターをミニポート ドライバーに渡します、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。 古いミニポート ドライバーは、可能な場合にのみ、このフラグを設定する必要があります。

-   これが必要となるすべてのハードウェアのコンテキストを保存します。

-   適切なスリープの状態 (D3) 状態にある NIC を配置します。

-   Highest-powered 状態 (D0) に NIC を再アクティブ化します。

NDIS は、NIC が管理に対応していないは電源し、ミニポート ドライバーでは、NDIS は設定しなかったかどうか、バス ドライバーから判断された場合に\_属性\_いいえ\_HALT\_ON\_SUSPEND フラグは、NDIS はクエリしません、ミニポート ドライバーの電源管理機能。 ただし、ミニポート ドライバーの設定、NDIS 場合\_属性\_いいえ\_停止\_ON\_SUSPEND フラグ、NDIS 問題、 [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)ミニポート ドライバーに要求します。 ここでは、ミニポート ドライバーの OID は成功\_PNP\_NDIS を使用して、機能要求\_状態\_成功します。 NDIS で\_PM\_WAKE\_を\_機能は、ミニポート ドライバーは、この要求に応答を返します、ミニポート ドライバーがのデバイスの電源状態を指定する必要がありますもこと構造体**NdisDeviceStateUnspecified**ウェイク アップ機能ごと。

NDIS は、古いミニポート ドライバーに次の電源管理のサポートを提供します。

-   NDIS は、すべてが成功した[ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699) NIC を表すオブジェクトをシステム電源マネージャーがデバイスに送信した要求 NDIS を保証するミニポート ドライバーの NIC が状態に移行 D3 の IRP に応答\_MN\_クエリ\_システムから電源要求。

-   ミニポート ドライバーでは、NDIS を設定しなかった場合、\_属性\_いいえ\_HALT\_ON\_SUSPEND フラグ NDIS の初期化中に呼び出し、ミニポート ドライバーの[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)ミニポート ドライバーの NIC の前に関数が D3 の状態に遷移します。 ミニポート ドライバーの NIC には、すべてのハードウェアのコンテキスト情報が失われます。

-   ミニポート ドライバーの設定、NDIS 場合\_属性\_いいえ\_HALT\_ON\_NDIS の初期化中に中断フラグ状態 D3 にシステム遷移する前に、ミニポート ドライバーは停止されません。 NDIS ミニポート ドライバーの問題、代わりに、 [OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780) D3 の状態を要求します。 ミニポート ドライバーを使用して任意のハードウェアのコンテキストを保存し、NIC を D3 状態に適した状態で配置する必要があります。

-   システムが、S0 に遷移するときに[システム電源の状態](https://msdn.microsoft.com/library/windows/hardware/ff564571)、NDIS ミニポート ドライバーの呼び出す[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) NDIS ミニポートを停止した場合の関数ドライバー。 NDIS ミニポート ドライバーを停止されませんでしたと OID に NDIS 問題が、ミニポート ドライバー\_PNP\_設定\_d0 へ POWER 要求。 ミニポート ドライバーする必要があります状態になる NIC D0 状態の適切です。

-   場合は、ミニポート ドライバーが停止され、再初期化、NDIS は OID 要求を発行して適切なミニポート ドライバー、すべての設定など、パケット フィルターおよびマルチキャスト アドレスのリストを復元します。 ミニポート ドライバーがない停止され、再初期化し場合、ミニポート ドライバーは、このような設定を復元する必要があります。

 

 





