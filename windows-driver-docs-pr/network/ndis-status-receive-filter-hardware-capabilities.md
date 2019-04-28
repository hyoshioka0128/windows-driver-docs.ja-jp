---
title: NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: ミニポート ドライバーは、そのハードウェア フィルター機能の変更を受信するときに、NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES 状態を示す値を発行します。
ms.assetid: 12F7A736-D85A-4BB6-89E6-55195B76C29F
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 258db7d1a2e6e1367bec0d6d87ebfed6b0a18b81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363053"
---
# <a name="ndisstatusreceivefilterhardwarecapabilities"></a>NDIS\_状態\_受信\_フィルター\_ハードウェア\_機能


ミニポート ドライバーの問題、 **NDIS\_状態\_受信\_フィルター\_ハードウェア\_機能**ハードウェアのフィルター処理を受信するときの状態表示機能を変更します。 これらの機能には、INF ファイルの設定、または、現在無効になっているハードウェア機能が含まれる、**詳細**プロパティ ページ。

**注**  この状態の表示は、ミニポート ドライバーのサポート NDIS フィルターが表示されることによってのみ実行する必要があります。

 

ミニポート ドライバーはこの状態表示を行うときに、設定、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体へのポインターを[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。 フィルター処理機能を現在有効では、この構造が表示されるドライバーを初期化します。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

ミニポート ドライバーの問題、 **NDIS\_状態\_受信\_フィルター\_ハードウェア\_機能**ときは、次の条件のいずれかの状態表示true の場合:

-   ハードウェアは、1 つのネットワーク アダプターのフィルター機能の変更を受信します。 たとえば、受信フィルターを有効になっているまたは独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションで無効になっていることができます。

-   ハードウェアは、負荷分散マルチプレクサー中間ドライバーによって管理されているネットワーク アダプターのフェールオーバー (LBFO) チームのフィルター機能の変更を受信します。 たとえば、ハードウェア受信のフィルターのアダプターを追加またはチームから削除されたときに機能が変わる可能性があります。

    詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566498)します。

ミニポート ドライバーが発行するとき、次の手順を次の**NDIS\_状態\_受信\_フィルター\_ハードウェア\_機能**状態を示す値。

1.  ミニポートを初期化します、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)で現在有効になっている受信フィルター機能を持つ構造体ネットワーク アダプター。

    ミニポート ドライバーを初期化します、**ヘッダー**メンバー、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_フィルター\_機能\_リビジョン\_2および**サイズ**NDIS メンバー\_SIZEOF\_受信\_フィルター\_機能\_リビジョン\_2。

2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体の次のように状態の表示。

    -   **StatusCode**にメンバーを設定する必要があります[ **NDIS\_状態\_受信\_フィルター\_現在\_機能**](ndis-status-receive-filter-current-capabilities.md).

    -   **StatusBuffer**メンバーのアドレスに設定する必要があります、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

    -   **StatusBufferSize**にメンバーを設定する必要があります`sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)`します。

3.  ミニポート ドライバーが呼び出すことによって、状態を示す値を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。

**注**  重なってドライバーを使用できます、 **NDIS\_状態\_受信\_フィルター\_ハードウェア\_機能**状態現在有効な決定を示す値には、ネットワーク アダプターのフィルター機能が表示されます。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_受信\_フィルター\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569791)ハードウェア フィルター機能での受信を取得するには任意の時刻。

 

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

 

 




