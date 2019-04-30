---
title: OID_NDK_SET_STATE
description: セットの要求として NDIS および上にあるドライバーは、ミニポート アダプターの NDK 機能の状態を設定するのに OID_NDK_SET_STATE OID を使用します。
ms.assetid: 5BA49F42-FE37-4860-B68F-92A7F4007639
ms.date: 08/08/2017
keywords: -OID_NDK_SET_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d8fe2aad2183e158d6f04865357cee9abe3938a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391649"
---
# <a name="oidndksetstate"></a>OID\_NDK\_設定\_状態


セットの要求では、NDIS および上にあるドライバーを使用、OID\_NDK\_設定\_状態 OID ミニポート アダプターの NDK 機能の状態を設定します。

NDIS 6.30 と以降のミニポート ドライバー NDK サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

NDIS 問題では、この OID、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体を指す、 **ブール**と**InformationBufferLength**メンバー sizeof と等しく (**ブール**)。

-   場合、**ブール**値は**TRUE**と **\*NetworkDirect**キーワード値が 0 以外の場合、ミニポート アダプターの NDK 機能を有効にする必要があります。

    ミニポート ドライバーが読み取ることができます、  **\*NetworkDirect**キーワードの値によって、次の手順します。

    1.  呼び出す[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717) NDIS 処理を[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)関数で返されるときに、ミニポート ドライバーが初期化されました。 呼び出し元の詳細については**NdisOpenConfigurationEx**を参照してください[NDIS 6.0 のミニポート ドライバーでレジストリを読み取る](https://msdn.microsoft.com/library/windows/hardware/ff570429)します。

    2.  呼び出す[**エミュレーター**](https://msdn.microsoft.com/library/windows/hardware/ff564511)を渡して。

        -   "\*NetworkDirect"用、*キーワード*パラメーター

        -   **NdisParameterInteger**の*ParameterType*パラメーター

-   場合、**ブール**値は**FALSE**、ミニポート アダプタの NDK 機能を無効にする必要があります。

有効または無効では、NDK 機能、ミニポート ドライバーに[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)コールバック関数が」の手順に従う必要があります[の有効化とNDK機能を無効にします。](https://msdn.microsoft.com/library/windows/hardware/dn163547).

**注**  NDK 対応のミニポート ドライバーに呼び出す必要がありますしない[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)のコンテキストからその[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、ため、デッドロックが発生する可能性があります。 代わりに、呼び出す必要があります、 **NdisMNetPnPEvent**から他のコンテキストまたはキュー作業項目。

 

NDK 対応のミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数が返す必要があります**状態\_成功**OID の\_NDK\_設定\_状態 OID 要求エラーが発生しない限り、します。 ドライバーに返す必要がありますいない**NDIS\_状態\_PENDING**します。

<a name="requirements"></a>要件
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


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisMNetPnPEvent**](https://msdn.microsoft.com/library/windows/hardware/ff563616)

[**NdisQueueIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff563775)

[**NdisReadConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564511)

[**NDK\_ADAPTER**](https://msdn.microsoft.com/library/windows/hardware/hh439848)

[OID\_NDK\_SET\_STATE](oid-ndk-set-state.md)

 

 




