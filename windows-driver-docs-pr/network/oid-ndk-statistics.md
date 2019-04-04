---
title: OID_NDK_STATISTICS
description: クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID_NDK_STATISTICS OID ミニポート アダプターの NDK 統計情報を取得します。
ms.assetid: 30F16DEC-AEE6-49D4-8599-95374ACBD446
ms.date: 08/08/2017
keywords: -OID_NDK_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d4a077454e36a151fa862af3391538908b106d12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581799"
---
# <a name="oidndkstatistics"></a>OID\_NDK\_統計情報


クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID\_NDK\_統計 OID ミニポート アダプターの NDK 統計情報を取得します。

NDIS 6.30 と以降のミニポート ドライバー NDK サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

**注**  NDIS OID 要求インターフェイスを直接この OID をサポートしています。 直接の OID 要求インターフェイスの詳細については、[NDIS 6.1 Direct OID 要求インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff564736)を参照してください。

 

<a name="remarks"></a>コメント
-------

NDIS 問題では、この OID、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体を指す、 [**NDIS\_NDK\_統計\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451567)構造体。

NDK 対応のミニポート ドライバーを提供する必要があります、 **CounterSet**は、メンバー、 [ **NDIS\_NDK\_パフォーマンス\_カウンター** ](https://msdn.microsoft.com/library/windows/hardware/hh451565)構造体。

カウンターがなどのツールに発行される[perfmon](https://technet.microsoft.com/library/cc731067.aspx) (を参照してください、 [NetworkDirect アクティビティ](https://technet.microsoft.com/library/hh997022.aspx)パフォーマンス カウンター) され、パフォーマンス データ ヘルパー (PDH) とパフォーマンスのプログラムで利用できますライブラリ (PERFLIB) プログラミング インターフェイスです。 これらのインターフェイスの詳細については、[パフォーマンス カウンター](https://msdn.microsoft.com/library/windows/desktop/aa373083)を参照してください。

これらのカウンターは、呼び出すことによっても使用可能な[Get NetAdapterStatistics](https://technet.microsoft.com/library/jj130889) PowerShell コマンドレットを**RdmaStatistics**属性。 詳細については、 **RdmaStatistics**属性は、「 [ **MSFT\_NetAdapterStatisticsSettingData**](https://msdn.microsoft.com/library/hh872390)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>サポートなし</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[カーネル モードのパフォーマンスの監視](https://msdn.microsoft.com/library/windows/hardware/ff548159)

[**NDIS\_NDK\_パフォーマンス\_カウンター**](https://msdn.microsoft.com/library/windows/hardware/hh451565)

[**NDIS\_NDK\_統計\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451567)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




