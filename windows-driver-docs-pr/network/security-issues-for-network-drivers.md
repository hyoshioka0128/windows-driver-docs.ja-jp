---
title: ネットワーク ドライバーのセキュリティの問題
description: ここでは、ネットワークドライバーに固有のセキュリティの問題について説明します。
ms.assetid: 04400213-9bd4-4dbe-b302-24917450829f
keywords:
- ネットワークドライバー WDK、セキュリティ
- セキュリティ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9677778e08ad80f2315d47fe3889a489d9d8d646
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841990"
---
# <a name="security-issues-for-network-drivers"></a>ネットワーク ドライバーのセキュリティの問題

セキュリティで保護されたドライバーの作成に関する一般的な説明については、「[信頼できるカーネルモードドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)」を参照してください。

セキュリティを強化するために、次のような安全なコーディング方法とデバイスドライバーの一般的なガイダンスに加えて、ネットワークドライバーは次のことを行う必要があります。

- すべてのネットワークドライバーは、レジストリから読み取った値を検証する必要があります。 具体的には、 [**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)または[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)の呼び出し元は、レジストリから読み取られた値についての想定を作成することはできません。また、読み取る各レジストリ値を検証する必要があります。 **NdisReadConfiguration**の呼び出し元が、値が範囲外であると判断した場合は、代わりに既定値を使用する必要があります。 値が範囲外であることが**NdisReadNetworkAddress**の呼び出し元によって判断された場合は、代わりに、永続的な中程度のアクセス制御 (MAC) アドレスまたは既定のアドレスを使用する必要があります。

## <a name="oid-specific-issues"></a>OID 固有の問題

- ミニポートドライバーは、ミニ[*Portoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数または[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数の中で、ドライバーが設定するように要求されたオブジェクト識別子 (OID) の値を検証する必要があります。 設定する値が範囲外であるとドライバーによって判断された場合、設定された要求は失敗します。 オブジェクト識別子の詳細については、「[ミニポートドライバー情報の取得と設定」および「WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)」を参照してください。

- 中間ドライバーの*Miniportoidrequest*関数が、基になるミニポートドライバーに設定操作を渡さない場合、関数は OID 値を検証する必要があります。 詳細については、「[中間ドライバーのクエリと設定の操作](intermediate-driver-query-and-set-operations.md)」を参照してください。

### <a name="query-oid-security-guidelines"></a>クエリ OID のセキュリティガイドライン

ほとんどのクエリ Oid は、システム上の任意のモードアプリケーションで発行できます。 クエリ Oid については、次のガイドラインに従ってください。

1. バッファーのサイズが出力に十分な大きさであることを常に検証します。 出力バッファーサイズチェックのないすべてのクエリ OID ハンドラーには、セキュリティのバグがあります。

    ```c++
    if (oid->DATA.QUERY_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        oid->DATA.QUERY_INFORMATION.BytesNeeded = sizeof(ULONG);
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 常に、必ず正しい最小値と最小値を書き込みます。 これは、次の例のように `oid->BytesWritten = oid->InformationBufferLength` を割り当てるための赤いフラグです。

    ```c++
    // ALWAYS WRONG
    oid->DATA.QUERY_INFORMATION.BytesWritten = DATA.QUERY_INFORMATION.InformationBufferLength; 
    ```

    OS は、BytesWritten だバイトを、モードのアプリケーションにコピーします。 バイトが書き込まれたが、ドライバーが実際に書き込んだバイト数より大きい場合、OS は初期化されていないカーネルメモリを、情報漏えいの脆弱性であるモードにコピーします。 代わりに、次のようなコードを使用します。

    ```c++
    oid->DATA.QUERY_INFORMATION.BytesWritten = sizeof(ULONG);
    ``` 

3. バッファーから値を読み取らないようにします。 場合によっては、OID の出力バッファーが悪意のあるモードプロセスに直接マップされることがあります。 悪意のあるプロセスは、書き込んだ後に出力バッファーを変更できます。 たとえば、次のコードは攻撃を受ける可能性があります。これは、攻撃者が記述された NumElements を変更できるためです。

    ```c++
    output->NumElements = 4;
    for (i = 0 ; i < output->NumElements ; i++) {
        output->Element[i] = . . .;
    }
    ```
    バッファーからの読み取りを回避するには、ローカルコピーを保持します。 たとえば、上の例を修正するには、新しいスタック変数を導入します。

    ```c++
    ULONG num = 4;
    output->NumElements = num;
    for (i = 0 ; i < num; i++) {
        output->Element[i] = . . .;
    }
    ```

    この方法では、for ループは、出力バッファーからではなく `num` ドライバーのスタック変数から読み取りを行います。 また、ドライバーは、出力バッファーを `volatile` キーワードでマークして、コンパイラがこの修正を暗黙的に元に戻すことができないようにする必要があります。

### <a name="set-oid-security-guidelines"></a>OID セキュリティガイドラインの設定

ほとんどの Set Oid は、管理者またはシステムセキュリティグループで実行されているモードのアプリケーションで発行できます。 これらは一般に信頼されているアプリケーションですが、ミニポートドライバーでは、メモリの破損やカーネルコードの注入を許可しない必要があります。 次の特定の規則に従って、Oid を設定します。

1.  入力が十分な大きさであることを常に検証します。 入力バッファーサイズチェックのない OID セットハンドラーには、セキュリティ上の脆弱性があります。

    ```c++
    if (oid->DATA.SET_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 埋め込みオフセットを使用して OID を検証するたびに、埋め込みバッファーが OID ペイロード内にあることを検証する必要があります。 これにはいくつかのチェックが必要です。 たとえば、 [OID_PM_ADD_WOL_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)は、チェックする必要がある埋め込みパターンを提供する場合があります。 正しい検証にはチェックが必要です:

    1. InformationBufferSize > = sizeof (NDIS_PM_PACKET_PATTERN)

        ```c++
        PmPattern = (PNDIS_PM_PACKET_PATTERN) InformationBuffer;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN))
        {
            Status = NDIS_STATUS_BUFFER_TOO_SHORT;
            *BytesNeeded = sizeof(NDIS_PM_PACKET_PATTERN);
            break;
        }
        ```

    2. Pattern-> PatternOffset + Pattern-> pattern のサイズがオーバーフローしません

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternSize, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

        この2つのチェックは、次の例のようなコードを使用して組み合わせることができます。

        ```c++
        ULONG TotalSize = 0;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN) ||
            !NT_SUCCESS(RtlUlongAdd(Pattern->PatternSize, Pattern->PatternOffset, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
    3. InformationBuffer + Pattern-> PatternOffset + Pattern-> pattern の長さがオーバーフローしません

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            (!NT_SUCCESS(RtlUlongAdd(TotalSize, InformationBuffer, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

    4. Pattern-> PatternOffset + Pattern-> pattern Length < = InformationBufferSize

        ```c++
        ULONG TotalSize = 0;
        if(!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            TotalSize > InformationBufferLength)) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
### <a name="method-oid-security-guidelines"></a>メソッド OID のセキュリティガイドライン

メソッド Oid は、管理者またはシステムセキュリティグループで実行されているモードのアプリケーションで発行できます。 これらはセットとクエリの組み合わせであるため、上記のガイダンスリストはどちらもメソッド Oid に適用されます。

## <a name="other-network-driver-security-issues"></a>ネットワークドライバーのセキュリティに関するその他の問題

- 多くの NDIS ミニポートドライバーは、NdisRegisterDeviceEx を使用してコントロールデバイスを公開します。 これを行う場合は、WDM ドライバーと同じセキュリティ規則をすべて使用して、IOCTL ハンドラーを監査する必要があります。 詳細については、「 [I/o 制御コードのセキュリティの問題](https://docs.microsoft.com/windows-hardware/drivers/kernel/security-issues-for-i-o-control-codes)」を参照してください。

- 適切に設計された NDIS ミニポートドライバーは、特定のプロセスコンテキストでの呼び出しに依存したり、アクセス操作と密接に対話したりすることはできません (Ioctl & Oid は例外です)。 この赤いフラグは、モードハンドルを開いたミニポートを表示したり、モードの待機を実行したり、モードクォータに対して割り当てられたメモリを確認したりするためのものです。 このコードは調査する必要があります。

- ほとんどの NDIS ミニポートドライバーは、パケットペイロードの解析に関係しないようにする必要があります。 ただし、場合によっては、これが必要になることがあります。 その場合、ドライバーが信頼できないソースからのデータを解析しているため、このコードを慎重に監査する必要があります。

- カーネルモードのメモリを割り当てるときの標準と同様に、NDIS ドライバーでは適切な[NX プールのオプトインメカニズム](https://docs.microsoft.com/windows-hardware/drivers/kernel/nx-pool-opt-in-mechanisms)を使用する必要があります。 WDK 8 以降では、`NdisAllocate*` ファミリの関数が適切にオプトインされています。

