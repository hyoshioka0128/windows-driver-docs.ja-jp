---
title: OID_WWAN_REGISTER_STATE
description: OID_WWAN_REGISTER_STATE を登録するネットワーク プロバイダーを選択します。
ms.assetid: 564de5bf-10d9-47fe-a4c1-3409d9b2aee8
ms.date: 08/08/2017
keywords: -OID_WWAN_REGISTER_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6d453e4956a330ee08ded409b1263c71d8c25f75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549274"
---
# <a name="oidwwanregisterstate"></a>OID\_WWAN\_登録\_状態


OID\_WWAN\_登録\_状態を登録するネットワーク プロバイダーを選択します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_登録\_状態**](ndis-status-wwan-register-state.md)状態通知を含む、 [ **NDIS\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567917)セットの完了に関係なく、登録されているネットワーク プロバイダーに関する情報を提供または要求をクエリする構造体。

ネットワーク プロバイダーに登録を設定するように要求して呼び出し元に提供する[ **NDIS\_WWAN\_設定\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567926)構造体を適切な情報のミニポート ドライバー。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN 登録操作](https://msdn.microsoft.com/library/windows/hardware/ff559116)します。

ミニポート ドライバーは、処理するときに、プロバイダーのネットワークにアクセスできるクエリまたはの集合演算、Subscriber Identity Module (SIM カード) にアクセスしないでください。

MB ドライバー モデルは、-自動および手動の 2 つの登録メソッドをサポートします。 CDMA ベースのネットワークでは、MB ドライバー モデルでは、自動登録のみをサポートしています。

手動で登録をサポートしているデバイスを設定する必要があります、 **WwanControlCaps**メンバー [ **WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff571204) WWAN構造体\_Ctrl キーを押し\_CAP\_REG\_手動です。 GSM ベースのデバイスが手動で登録をサポートする必要がありますに注意します。

登録の状態が自動の場合は、ミニポート ドライバーには、デバイスを携帯電話テクノロジに固有の選択アルゴリズムに基づくネットワーク プロバイダーを選択し、登録を続行する必要がありますように指示します。

RegisterAction 値のセマンティクスの定義は次のとおりです。

-   *WwanRegisterActionAutomatic*フラグは、デバイスを登録する自動モードに設定し、最適なプロバイダー ネットワークを選択して、デバイスをミニポート ドライバーに指示する MB サービスによって使用されます。 ミニポート ドライバーを無視する必要があります**ProviderId**パラメーター。 この設定は、オプションの状態 (オン/オフ) の間で永続的なとが明示的になるまで、デバイスの電源サイクルが MB サービスによって変更します。

-   *WwanRegisterActionManual* MB サービスによってミニポート ドライバーで識別される、プロバイダーのネットワークを登録するように指示するフラグが使用される、 **ProviderId**パラメーター。 **ProviderId**値に由来は、 **ProviderId** WWAN のメンバー\_表示されているプロバイダーのいずれかのプロバイダー データ構造体。 MB サービスによって、明示的に変更されるまで、この設定はオプションの状態 (オン/オフ) と、デバイスの電源サイクルの間で永続的なです。

-   デバイスがプロバイダーに現在登録されている場合でも、異なる RegisterAction 値間の切り替えが許可されます。 デバイスは、自動と手動登録モードの切り替え前に、の登録を解除する場合に、ミニポート ドライバーは、デバイスが新しい登録モードに設定する前に登録解除に設定されていることを確認する必要があります。

-   *手動*と*自動*登録モードでは、ネットワークの選択モードのみに影響します。 MB デバイスは、無線がオンになっているときに、選択したネットワークに登録しようとする必要があります。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_設定\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567926)

[**NDIS\_状態\_WWAN\_登録\_状態**](ndis-status-wwan-register-state.md)

[WWAN 登録操作](https://msdn.microsoft.com/library/windows/hardware/ff559116)

 

 




