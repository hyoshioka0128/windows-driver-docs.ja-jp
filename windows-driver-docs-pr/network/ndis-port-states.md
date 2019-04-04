---
title: NDIS ポートの状態
description: NDIS ポートの状態
ms.assetid: bb13edd2-815b-488a-b36c-21a48809a143
keywords:
- WDK NDIS、状態のポート
- NDIS ポート WDK、状態
- WDK NDIS ポートの状態
- 認証は、WDK NDIS ポートを状態します。
- リンク状態 WDK NDIS ポート
- 初期化状態 WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be46838e27f92691ad8faf299fc028a3f906dfa0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572164"
---
# <a name="ndis-port-states"></a>NDIS ポートの状態





NDIS ポートがある動作の初期化状態で指定されている状態は、状態、 [ **NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)構造体。 ポートの状態は、次のカテゴリに合わせます。

<a href="" id="initialization-states"></a>初期化状態  
NDIS ポートの状態は、スタートアップの初期化に関連付けられているし、プラグ アンド プレイ (PnP) イベントに初期化します。 NDIS またはミニポート ドライバーは、最初にポートを割り当てますとき、に、ポートが、*割り当てられている状態*します。 NDIS またはミニポート ドライバーにポートがアクティブ化した後にポートが、*状態をアクティブ化される*します。 非アクティブなポートことはできません送受信したりデータ、状態インジケーターを作成、OID の要求を受信したり PnP イベントを開始します。

<a href="" id="link-states"></a>リンクの状態  
NDIS ポート リンクの状態はミニポート アダプターに関連付けられているしで指定された状態のリンクに似ています、 [ **NDIS\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh205390)構造体。 ポートのリンクの状態は、メディア リンクの接続状態とのリンク速度を示します。 ポートのリンクの状態は、関連付けられているミニポート アダプターのリンクの状態を異なっていてもかまいません。

<a href="" id="authentication-states"></a>認証の状態  
NDIS ポート認証の状態、ポートが制御されるかどうかを示します (承認が必要)、データ転送の方向 (send、receive、またはその両方)、およびポート (承認または許可されていません) の承認の状態。 ポートが制御されていない場合は、認証と、未認証の状態は無視されます。

ミニポート ドライバーでは、ポートをアクティブ化したり、PnP イベントでのポートを非アクティブ化することができます。 アクティブ化して、ポートを非アクティブ化の詳細については、[ライセンス NDIS ポート](activating-an-ndis-port.md)と[Deactivating NDIS ポート](deactivating-an-ndis-port.md)を参照してください。

ドライバーの使用が重なって、 [OID\_GEN\_ポート\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569624)で指定されているポートの現在の状態を取得する OID、 **PortNumber** のメンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS が、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS ポートをサポートするミニポート ドライバーを使用する必要があります、 [ **NDIS\_状態\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567415) NDIS ポートの状態の変化を示すステータスを示す値。 ミニポート ドライバー ポート番号を設定する必要があります、 **PortNumber**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。

NDIS および上にあるドライバーを使用して、 [OID\_GEN\_ポート\_認証\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569623) NDIS ポートの現在の認証状態を設定する OID。 NDIS ポートをサポートするミニポート ドライバーでは、この OID をサポートする必要があります。

 

 





