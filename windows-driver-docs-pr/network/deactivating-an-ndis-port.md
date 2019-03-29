---
title: NDIS ポートの非アクティブ化
description: NDIS ポートの非アクティブ化
ms.assetid: 2a5d288f-b6ea-4b63-91a3-44155aae8064
keywords:
- ポート WDK NDIS、非アクティブ化
- NDIS ポート WDK、非アクティブ化
- WDK NDIS をポート NDIS を非アクティブ化
- 非アクティブ化の PnP イベント WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06659c1d44b1b038db1da1a56b2cde61a9aad544
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572174"
---
# <a name="deactivating-an-ndis-port"></a>NDIS ポートの非アクティブ化





NDIS ポートを非アクティブ化には、ミニポート ドライバーは、NDIS にポートの非アクティブ化プラグ アンド プレイ (PnP) イベントを送信します。 ミニポート ドライバーにポートが正常にアクティブ化した後、ドライバーする必要がありますを非アクティブ化ポート前に、そのポートを解放することができます。 また、ドライバーには、アプリケーション固有の理由のポートが非アクティブ化可能性があります。 非アクティブ化が解放される場合は、ポートを再アクティブ化できません後は、ポートを再びアクティブにできます。

ポートの非アクティブ化の PnP イベントを送信するミニポート ドライバーを使用して、 **NetEventPortDeactivation**イベント コードの呼び出しでの PnP、 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)関数。 ミニポート ドライバー、ポートを無効にするのメンバーを設定する必要があります、 [ **NET\_PNP\_イベント\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)構造体、 *NetPnPEvent*パラメーターの**NdisMNetPnPEvent**を次のようにポイントします。

<a href="" id="portnumber"></a>**PortNumber**  
イベント通知の送信元ポート。 ポート番号がで提供されるため、このメンバーを 0 に設定、**バッファー** 、構造体のメンバーを**NetPnPEvent**メンバーを指定します。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
A [ **NET\_PNP\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff568751)ポートの非アクティブ化イベントを記述する構造体。 この構造体のメンバーを次のように設定します。

<a href="" id="netevent"></a>**NetEvent**  
イベントを説明するイベント コードを指定します。 このメンバーを設定**NetEventPortDeactivation**します。

<a href="" id="buffer"></a>**バッファー**  
NDIS の配列へのポインター\_ポート\_数の型の要素。 配列には、ミニポート ドライバーを非アクティブ化するポートのすべてのポート番号が含まれています。

<a href="" id="bufferlength"></a>**BufferLength**  
指定されているバイト数**バッファー**します。 設定**BufferLength** 、配列のサイズを**バッファー**を指します。 配列内の要素の数を取得するには、値を除算**BufferLength** NDIS のサイズによって\_ポート\_数値データ型。

<a href="" id="other-members"></a>他のメンバー  
NET の残りのメンバーを設定\_PNP\_イベント**NULL**します。

ミニポート ドライバーでは、非アクティブ化するポートの一覧を含む配列を提供できます。 ただし、ミニポート アダプターの既定のポートのターゲットであるかどうか、 **NetEventPortDeactivation** PnP イベントは、既定のポートは、配列で指定されている唯一のポートである必要があります。

ミニポート ドライバーは、いつでも、アクティブなポートを非アクティブ化できます。 ただし、ミニポート ドライバーには、ポートが非アクティブ化、前に、未処理の状態インジケーターがないまたは受信ポートに関連付けられている表示があることが確認する必要があります。 ミニポート ドライバーが、ポートの非アクティブ化の PnP イベントを送信した後、すべての状態を開始または受信ポートを非アクティブ化に関連付けられている表示しないください。

ミニポート ドライバーには、ポートも再アクティブ化できます。 NDIS ポートをアクティブ化についての詳細については、次を参照してください。[ライセンス NDIS ポート](activating-an-ndis-port.md)します。

NDIS ミニポート ドライバーにバインドされているプロトコル ドライバーのすべてに通知ミニポート ドライバーには、ポートが非アクティブ化、ときに、 **NetEventPortDeactivation** PnP イベント。 この PnP イベントでは、ポートが割り当てられている状態に変更され、ポートは既に非アクティブ化するには含まれませんが一覧表示します。 プロトコル ドライバーでのポートの非アクティブ化イベントの処理の詳細については、次を参照してください。[ポート非アクティブ化の PnP イベントを処理する](handling-the-port-deactivation-pnp-event.md)します。

ミニポート ドライバーは、NDIS ポートを割り当てる、前に、ドライバーを呼び出す必要があります、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)の登録を設定する関数の属性、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ミニポート ドライバーは、NDIS を設定して、既定のポートのアクティブ化を制御できます\_ミニポート\_コントロール\_既定\_ポート属性フラグの呼び出し時に**NdisMSetMiniportAttributes**. 戻る前に、既定のポートを無効する必要がありますミニポート ドライバーには、既定のポートをアクティブ化を担当し、ミニポート ドライバーには、既定のポートがアクティブ化される場合、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数。

すべての NDIS の配列で指定されているポート\_ポート\_要素の数がアクティブ化された状態である必要があります。 ミニポート ドライバーは、ポートが既に非アクティブ化を非アクティブ化しないようにします。

NDIS は、ポート配列内の任意のポートを非アクティブ化に失敗すると、ポート配列内のポートは状態を変更します。 指定したポートの一部が存在しないため、非アクティブ化に失敗した場合、 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)関数は、NDIS を返します\_状態\_無効な\_ポート値を返します。 ポートの一部がアクティブ化された状態でないため、非アクティブ化に失敗した場合**NdisMNetPnPEvent**返します NDIS\_状態\_無効な\_ポート\_状態の戻り値。

呼び出されるまで、 **NdisMNetPnPEvent**返します、ポートが非アクティブ化しないと、ミニポート ドライバーは、OID 要求を処理し、そのポートに関連付けられている要求を送信することである必要があります。

ミニポート ドライバーには、既定のポートが非アクティブ化、すべての上位のプロトコル ドライバーとミニポート アダプター間のバインド NDIS 終了します。 場合、ミニポート ドライバーの既定のポートを非アクティブ化しようとして、既定のポートは既に非アクティブ化、 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)は失敗し、NDIS を返します\_状態\_が無効です\_ポート\_状態の戻り値。 ミニポート ドライバーが既定のポートを非アクティブ化しようし、既定のポートは、NDIS の配列で指定されている唯一のポートではない場合\_ポート\_要素の数、 **NdisMNetPnPEvent**失敗し、返します、NDIS\_状態\_無効な\_ポートの戻り値。 ミニポート ドライバーが設定されている場合、**バッファー**メンバー **NULL**または**BufferLength**をゼロにメンバーは、NDIS 失敗、 **NdisMNetPnPEvent**を呼び出すとNDIS を返します\_状態\_無効な\_パラメーター値を返します。

ポートが正常に非アクティブ化した後、ポートが割り当て済みの状態です。 ミニポート ドライバーには、受信したデータまたは割り当てられている状態で、ポートの状態を示すことはできません。

 

 





