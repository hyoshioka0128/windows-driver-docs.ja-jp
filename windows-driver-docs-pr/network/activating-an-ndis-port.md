---
title: NDIS ポートをアクティブ化します。
description: NDIS ポートをアクティブ化します。
ms.assetid: 0f3bfda2-8faa-4a92-a76b-0c0c361bd667
keywords:
- ポート WDK NDIS、アクティブ化します。
- NDIS、WDK のポートをアクティブ化します。
- NDIS ポートをアクティブ化します。
- ポートの状態が WDK NDIS
- PnP イベント WDK NDIS ポートのアクティブ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69f6a88960f4de5b5d90052d8cf472a8017d04bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550382"
---
# <a name="activating-an-ndis-port"></a>NDIS ポートをアクティブ化します。





後のミニポート ドライバーは、NDIS ポートを正常に割り当てられ、NDIS 関数で、ポート番号を使用する前に、ポートがこのドライバーにアクティブ化する必要があります。 ポートを有効にするには、ミニポート ドライバーは、NDIS にポートのアクティブ化プラグ アンド プレイ (PnP) イベントを送信します。 ミニポート ドライバーを使用して、ポートのアクティブ化の PnP イベントを送信する、 **NetEventPortActivation**イベント コードの呼び出しでの PnP、 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)関数。

ポートを有効にするには、ミニポート ドライバーがのメンバーを設定する必要があります、 [ **NET\_PNP\_イベント\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)構造体、 *NetPnPEvent*パラメーターの**NdisMNetPnPEvent**を次のようにポイントします。

<a href="" id="portnumber"></a>**PortNumber**  
イベント通知の送信元ポート。 ポート番号がで提供されるため、このメンバーを 0 に設定、**バッファー** 、構造体のメンバーを**NetPnPEvent**メンバーを指定します。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
A [ **NET\_PNP\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff568751)ポートのアクティブ化イベントを記述する構造体。 この構造体のメンバーを次のように設定します。

<a href="" id="netevent"></a>**NetEvent**  
イベントを説明するイベント コードを指定します。 このメンバーを設定**NetEventPortActivation**します。

<a href="" id="buffer"></a>**バッファー**  
リンク リストへのポインター [ **NDIS\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff566769)構造体。 **次**NDIS のメンバー\_ポート構造 NDIS が [次へ] をポイント\_一覧にポートの構造。

<a href="" id="bufferlength"></a>**BufferLength**  
指定されているバイト数**バッファー**します。 設定**BufferLength** NDIS のサイズに\_ポート構造体。

<a href="" id="other-members"></a>他のメンバー  
NET の残りのメンバーを設定\_PNP\_イベント**NULL**します。

ミニポート ドライバーの一覧のリンク リスト内にアクティブから非アクティブな状態に変更されたポート[ **NDIS\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff566769)構造体。 ただし、ミニポート アダプターの既定のポートのターゲットであるかどうか、 **NetEventPortActivation** PnP イベントは、既定のポートは、リスト内唯一のポートである必要があります。

ミニポート ドライバーは、ポートがアクティブ化された NDIS に通知します (し、返します呼び出すこの通知が送信される可能性)、ミニポート ドライバーが要求を送信し、ポートに関連付けられている OID 要求を処理できる場合があります。 ミニポート ドライバーの状態で、新しくアクティブになったポートのポート番号を使用して、または受信呼び出しの後になるまで表示する必要がありますいない[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)を返します。

NDIS では、既定のポートがアクティブになった後までのアクティブ化されたポートの上にあるドライバーは通知されません。 NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体、 *BindParameters*パラメーターを指します。 ミニポート ドライバーでは、新しいポートがアクティブ化、すべてのミニポート ドライバーにバインドされているプロトコル ドライバーに通知 NDIS、 **NetEventPortActivation** PnP イベント。 プロトコル ドライバーでのこれらのポートのアクティブ化イベントの処理の詳細については、次を参照してください。[ポート アクティベーション PnP イベントを処理する](handling-the-port-activation-pnp-event.md)します。

ミニポート ドライバーは、NDIS ポートを割り当てる、前に、ドライバーを呼び出す必要があります、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)の登録を設定する関数の属性、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ミニポート ドライバーは、NDIS を設定して、既定のポートのアクティブ化を制御できます\_ミニポート\_コントロール\_既定\_ポート属性フラグの呼び出し時に**NdisMSetMiniportAttributes**. ミニポート ドライバーは、既定のポートをアクティブ化する責任を引き受けると場合、NDIS がミニポート ドライバーには、ポートのアクティブ化の PnP イベントで、既定のポートがアクティブになるまでミニポート アダプターと関連付けたドライバーの間のバインドを開始していません。

すべての NDIS のリンク リストで指定されているポート\_ポート構造体が割り当てられている状態である必要があります。 ミニポート ドライバーはアクティブになっているポートをアクティブ化しようとはしないでください。場合は、ドライバーは NDIS treates ポートのアクティブ化エラーと状況、アクティブなポートをアクティブ化しようとしています。

呼び出しが失敗する NDIS は、一覧の任意のポートをアクティブ化に失敗した場合、 [ **NdisMNetPnPEvent**](https://msdn.microsoft.com/library/windows/hardware/ff563616)、アクティブ化された状態に状態を変更リストにポート。 NDIS は、一部のポートが存在しないため、ポートをアクティブ化が失敗した場合**NdisMNetPnPEvent** 、NDIS 返します\_状態\_無効な\_ポートの戻り値。 NDIS は、割り当て済みの状態の一部のポートがないため、ポートをアクティブ化が失敗した場合**NdisMNetPnPEvent**返します、NDIS\_状態\_無効な\_ポート\_状態の戻り値.

ポートが正常にアクティブ化した後、ポートは、アクティブ化された状態です。 ミニポート ドライバーには、受信したデータとアクティブ化された状態で、ポートの状態を指定できます。

NDIS 通過する既定のポートの認証の状態、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の**DefaultPortAuthStates**のメンバー、 [**NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)構造体。 ミニポート ドライバーは、ミニポート ドライバーには、既定のポートがアクティブにしたときに、既定のポートを制御する場合は、既定の認証設定を使用して、既定のポートをアクティブ化できます。 既定の認証設定を使用する設定、NDIS\_ポート\_CHAR\_使用\_既定\_AUTH\_でフラグを設定、**フラグ**のメンバー[ **NDIS\_ポート\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566791)構造体。 ミニポート ドライバーは、NDIS を使用できます\_ポート\_CHAR\_を使用して、\_既定\_AUTH\_割り当てとアクティブ化を行うポートのフラグを設定します。 NDIS ライセンス認証の場合、既定の認証状態が新しくアクティブになったポートに割り当てるし、に渡される認証の状態を無視[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)の**NetEventPortActivation**イベント。

既定のポートを制御して、ポートの割り当ての詳細については、次を参照してください。[割り当て NDIS ポート](allocating-an-ndis-port.md)します。

 

 





