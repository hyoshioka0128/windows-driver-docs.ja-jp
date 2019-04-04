---
title: OID_WWAN_HOME_PROVIDER
description: OID_WWAN_HOME_PROVIDER は設定し、携帯電話サービス サブスクリプションのホーム プロバイダーに関する情報を取得するために使用します。
ms.assetid: f7bea146-261d-4d01-9fd5-ae512a1ac083
ms.date: 08/08/2017
keywords: -OID_WWAN_HOME_PROVIDER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bb86023c594a1cfad4f7a6153e6fab7f828f5477
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552436"
---
# <a name="oidwwanhomeprovider"></a>OID\_WWAN\_ホーム\_プロバイダー


OID\_WWAN\_ホーム\_プロバイダーが使用して設定し、携帯電話サービス サブスクリプションのホーム プロバイダーに関する情報を取得します。 GSM ベースのデバイスと U RIM で CDMA ベースのデバイスでは、この情報は、Subscriber Identity Module (SIM カード) に格納する必要があります。 U RIM せず CDMA ベースのデバイスの補助デバイスのメモリ内でこの情報を格納する必要があります。

Windows 8 では、両方をサポート*設定*と*クエリ*要求。 Windows 7 のサポートのみ*クエリ*要求。

ミニポート ドライバーの両方を処理する必要があります*設定*と*クエリ*NDIS を非同期的に、最初に返す要求\_状態\_INDICATION\_に必要な元の要求とそれ以降の送信、 [ **NDIS\_状態\_WWAN\_ホーム\_プロバイダー** ](ndis-status-wwan-home-provider.md)を用の状態の通知*クエリ*、または NDIS\_状態\_WWAN\_設定\_ホーム\_プロバイダー\_完了状態の通知、 *の設定*を含む、 [ **NDIS\_WWAN\_ホーム\_プロバイダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567909)構造体を使用して、ホーム ネットワーク プロバイダーに関する情報を返す**Provider.ProviderState**の NDIS メンバー\_WWAN\_ホーム\_WWAN 設定プロバイダーの構造体\_プロバイダー\_状態\_ホーム。

*設定*操作はマルチ キャリア対応のデバイスでサポートされなければならないのみ必要です。 MB サービスはのみ*設定*OID を使用してミニポートによってマルチ キャリアのプロバイダーに、ホーム プロバイダーが報告された\_WWAN\_優先\_マルチ\_プロバイダーまたは OID\_WWAN\_VISIBLE\_プロバイダー。 *設定*操作がある、入力バッファーの NDIS\_WWAN\_設定\_ホーム\_プロバイダー。

<a name="remarks"></a>注釈
-------

A*設定*操作では、現在の SIM またはターゲット SIM がロック状態の場合に関係なく、デバイスのロックを解除するユーザーは必要ありません。

| 現在のプロバイダー SIM | SIM のターゲット プロバイダー | 結果を*設定*ホーム\_プロバイダー                               |
|----------------------|---------------------|--------------------------------------------------------------|
| -                    | Locked (ロック)              | 暗証番号 (pin) のターゲットがホーム プロバイダーの設定では必要ありません。            |
| Locked (ロック)               | -                   | 暗証番号 (pin) のソースがホーム プロバイダーの設定では必要ありません。            |
| Locked (ロック)               | Locked (ロック)              | ソースとターゲットは、ホーム プロバイダーの設定は必要ありません暗証番号 (pin)。 |

 

詳細については、この OID を使用して、[WWAN プロバイダー操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)を参照してください。

ミニポート ドライバー Subscriber Identity Module (SIM カード) にアクセスできる処理がクエリ操作が、プロバイダーのネットワークにアクセスしないでください。

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


[**NDIS\_WWAN\_ホーム\_プロバイダー**](https://msdn.microsoft.com/library/windows/hardware/ff567909)

[**NDIS\_状態\_WWAN\_ホーム\_プロバイダー**](ndis-status-wwan-home-provider.md)

[WWAN プロバイダー操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)

 

 




