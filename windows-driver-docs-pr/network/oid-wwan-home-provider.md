---
title: OID_WWAN_HOME_PROVIDER
description: OID_WWAN_HOME_PROVIDER は、移動体通信サービスのサブスクリプションのホームプロバイダーに関する情報を設定および取得するために使用されます。
ms.assetid: f7bea146-261d-4d01-9fd5-ae512a1ac083
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_HOME_PROVIDER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3bee8cbfcb751534bca1248166b808274c72c4c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843841"
---
# <a name="oid_wwan_home_provider"></a>OID\_WWAN\_ホーム\_プロバイダー


OID\_WWAN\_ホーム\_プロバイダーは、携帯電話サービスのサブスクリプションのホームプロバイダーに関する情報を設定および取得するために使用されます。 GSM ベースのデバイスと、U フレームを使用した CDMA ベースのデバイスの場合、この情報はサブスクライバー Id モジュール (SIM カード) に保存する必要があります。 U フレームを使用しない CDMA ベースのデバイスの場合、この情報を補助デバイスメモリに格納する必要があります。

Windows 8 では、 *set*要求と*クエリ*要求の両方がサポートされています。 Windows 7 では、*クエリ*要求のみがサポートされます。

ミニポートドライバーは、 *set*要求と*クエリ*要求の両方を非同期に処理し、最初に ndis\_status\_を返して、元の要求に必要な\_を示し、後で ndis\_の状態を送信する必要があり[ **\_WWAN\_ホーム\_プロバイダー**](ndis-status-wwan-home-provider.md)の状態通知、*クエリ*、または NDIS\_ステータス\_wwan\_設定\_ホーム\_プロバイダー\_設定の完全な状態通知、*セット*、[**ndis\_wwan\_home\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)構造が含まれており、ホームネットワークプロバイダーに関する情報を**プロバイダーの providerstate**メンバーと共に取得します。 NDIS\_WWAN\_ホーム\_プロバイダーの構造が WWAN\_プロバイダー\_STATE\_HOME に設定されています。

*Set*操作は、マルチキャリア対応デバイスでのみサポートされている必要があります。 MB サービスでは、ホームプロバイダーを、ミニポートによって報告されたマルチキャリアプロバイダーに*設定*するのは、マルチキャリア\_プロバイダー、または oid\_\_の\_を\_使用して、ミニポートによって報告されます。 *Set*操作には、\_ホーム\_プロバイダー\_設定された NDIS\_WWAN の入力バッファーがあります。

<a name="remarks"></a>注釈
-------

*設定*操作では、現在の sim またはターゲット sim がロック状態であるかどうかに関係なく、ユーザーがデバイスのロックを解除する必要はありません。

| 現在のプロバイダー SIM | ターゲットプロバイダーの SIM | ホーム\_プロバイダーの*設定*の結果                               |
|----------------------|---------------------|--------------------------------------------------------------|
| -                    | [ロック]              | ホームプロバイダーの設定には、ターゲットの PIN は不要です            |
| [ロック]               | -                   | ホームプロバイダーの設定にソース PIN は必要ありません            |
| [ロック]               | [ロック]              | ホームプロバイダーの設定にソースとターゲットの PIN は不要です |

 

この OID の使用方法の詳細については、「 [WWAN プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)」を参照してください。

ミニポートドライバーは、クエリ操作を処理するときにサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーネットワークにはアクセスできません。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_ホーム\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)

[**NDIS\_ステータス\_WWAN\_ホーム\_プロバイダー**](ndis-status-wwan-home-provider.md)

[WWAN プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




