---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX は、OID_WWAN_DEVICE_CAPS から似ていますが、別の OID です。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_DEVICE_CAPS_EX、ex デバイスの機能、executor あたりの OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89347328408ea03295a7c1ddc2b9d35bb4d56abe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574581"
---
# <a name="oidwwandevicecapsex"></a>OID\_WWAN\_デバイス\_CAP\_例


OID\_WWAN\_デバイス\_CAP\_EX がからに似ていますが、別の OID [OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)します。 OID\_WWAN\_デバイス\_CAP\_EX が、実行プログラムあたり OID。 この OID を LTE 接続 APN 構成など、省略可能な機能の拡張機能を含む、ハードウェアのデバイス/実行プログラムの機能を示すためには機能します。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_後で送信する前に、元の要求に必要な[ **NDIS\_状態\_WWAN\_デバイス\_CAP\_EX** ](https://msdn.microsoft.com/library/windows/hardware/mt782396)状態通知を含む、 [ **NDIS\_WWAN\_デバイス\_CAP\_EX** ](https://msdn.microsoft.com/library/windows/hardware/mt782401)を格納する構造体、 [ **WWAN\_デバイス\_CAP\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt799889)構造体には、デバイスの機能に関する情報を提供します。

次の図は、クエリ要求を示しています。

![実行プログラムの機能のクエリ](images/multi-SIM_6_executorCapabilityQuery.png)

要求のセットには適用されません。

<a name="remarks"></a>コメント
-------

レポート サービスの拡張機能を実際のデバイス ドライバーを含む全体にドライバーが重要です。 ドライバーは、サービスをサポートしている基になるハードウェアでサポートされていない場合は、サービスの機能は FALSE としてマークする必要があります。

OID\_WWAN\_デバイス\_CAP\_EX は各 executor の機能の取得にも使用されます。 この OID は、既存の構造で同じ[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)が追加の**Executor ID**します。 ミニポート ドライバーでは、最上位の OID バージョンがサポートを報告する必要があります。

同様[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md)、SIM カードにより変更が選択された実行プログラムのモデムの RF の機能を表すではなくこの OID のパラメーターはありません。 物理ハードウェア モデムが複数の executor があり、そのため、OID をサポートする複数のインターフェイスを実装することがあります\_WWAN\_デバイス\_CAP\_エク.

今後の更新、OS の要求されたバージョンが、デバイスでサポートされているバージョンより新しい場合、デバイスはサポート OID 構造体の最新バージョンにする必要があります返します。 OS の要求されたバージョンが最新のデバイスでサポートされているものよりも古い場合は、デバイスは、OS の仕様に一致するバージョンを返す必要があります。 Ihv OID のすべての変更履歴を確認するための要件が\_WWAN\_デバイス\_CAP\_EX がサポートされているの下位互換性とレガシ サポートします。

その他の Oid を初めて使用する Windows 10 バージョン 1703 であるとは異なり、モデムがマルチ SIM/マルチ executor をサポートしている場合に必要なだけこの OID 実装する必要がある Windows 10 のバージョン以降では、Microsoft が定義したサービス拡張機能をサポートするモデム1703 します。

Windows 10 バージョン 1703 より前の Windows のバージョンがまだ既存を使用[OID\_WWAN\_デバイス\_CAP](oid-wwan-device-caps.md); マルチ executor 対応モデムでの動作がサポートされているシナリオではありません。 Ihv は、この動作を定義する必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_キャップ](oid-wwan-device-caps.md)

[**NDIS\_状態\_WWAN\_デバイス\_CAP\_例**](https://msdn.microsoft.com/library/windows/hardware/mt782396)

[**NDIS\_WWAN\_デバイス\_CAP\_例**](https://msdn.microsoft.com/library/windows/hardware/mt782401)

[**WWAN\_デバイス\_CAP\_例**](https://msdn.microsoft.com/library/windows/hardware/mt799889)



