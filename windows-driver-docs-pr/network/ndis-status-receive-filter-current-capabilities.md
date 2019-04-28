---
title: NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES
description: 現在、有効なフィルタ リング機能の変更を受信するときに、ミニポート ドライバーは NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES 状態を示す値を発行します。
ms.assetid: 6A1141A3-6E46-4A97-B482-CBE69E3D5075
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 600f330141fdec96ac179db42aed178967535aaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362858"
---
# <a name="ndisstatusreceivefiltercurrentcapabilities"></a>NDIS\_状態\_受信\_フィルター\_現在\_機能


ミニポート ドライバーの問題、 **NDIS\_状態\_受信\_フィルター\_現在\_機能**現在有効な受信状態の表示フィルター処理機能を変更します。

**注**  この状態の表示は、ミニポート ドライバーのサポート NDIS フィルターが表示されることによってのみ実行する必要があります。

 

ミニポート ドライバーはこの状態表示を行うときに、設定、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体へのポインターを[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。 フィルター処理機能を現在有効では、この構造が表示されるドライバーを初期化します。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

ミニポート ドライバーの問題、 **NDIS\_状態\_受信\_フィルター\_現在\_機能**次の条件のいずれかが true の場合、状態の表示:

-   現在有効になっている 1 つのネットワーク アダプターのフィルター機能の変更が表示されます。 たとえば、受信フィルターを有効になっているまたは独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションで無効になっていることができます。

-   現在有効になっている負荷分散マルチプレクサー中間ドライバーによって管理されているフェールオーバー (LBFO) のチームに属しているネットワーク アダプターを 1 つまたは複数のフィルター機能の変更が表示されます。 詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566498)します。

ミニポート ドライバーが発行するとき、次の手順を次の**NDIS\_状態\_受信\_フィルター\_現在\_機能**状態を示す値。

1.  ミニポートを初期化します、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)で現在有効になっている受信フィルター機能を持つ構造体ネットワーク アダプター。

    ミニポート ドライバーを初期化します、**ヘッダー**メンバー、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_フィルター\_機能\_リビジョン\_2および**サイズ**NDIS メンバー\_SIZEOF\_受信\_フィルター\_機能\_リビジョン\_2。

2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体の次のように状態の表示。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_受信\_フィルター\_現在\_機能**します。

    -   **StatusBuffer**メンバーのアドレスに設定する必要があります、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

    -   **StatusBufferSize**にメンバーを設定する必要があります`sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)`します。

3.  ミニポート ドライバーが呼び出すことによって、状態を示す値を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。

**注**  重なってドライバーを使用できます、 **NDIS\_状態\_受信\_フィルター\_現在\_機能**状態表示現在有効な受信ネットワーク アダプターのフィルター機能を確認します。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_受信\_フィルター\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569786)を取得する現在有効な受信フィルターいつでも機能します。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

[OID\_受信\_フィルター\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569786)

 

 




