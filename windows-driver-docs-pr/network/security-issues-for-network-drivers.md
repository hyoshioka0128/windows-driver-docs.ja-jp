---
title: ネットワークのドライバーに関するセキュリティの問題
description: このセクションには、ネットワーク ドライバーに固有のセキュリティの問題がについて説明します
ms.assetid: 04400213-9bd4-4dbe-b302-24917450829f
keywords:
- ネットワーク ドライバー WDK、セキュリティ
- WDK ネットワークのセキュリティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae0dc4ac862d4fadfae7b610923667dacfe90fc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530401"
---
# <a name="security-issues-for-network-drivers"></a>ネットワークのドライバーに関するセキュリティの問題

セキュリティで保護されたドライバーの記述の概要については、[信頼性の高いカーネル モード ドライバーの作成](https://msdn.microsoft.com/library/windows/hardware/ff542904)を参照してください。

次の安全なコーディング手法を全般的なデバイス ドライバーに関するガイダンスだけでなく、ネットワーク ドライバーはセキュリティを強化するために、次を実行してください。

- すべてのネットワーク ドライバーは、レジストリから読み取る必要が値を検証する必要があります。 具体的には、呼び出し元の[**エミュレーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564511)または[ **NdisReadNetworkAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff564512)についてどのような想定を行ってはいけません値は、レジストリから読み取られ、各レジストリ値を読み取ることを検証する必要があります。 場合、呼び出し元の**エミュレーター**値が範囲外です、既定値を代わりに使用することを決定します。 場合、呼び出し元の**NdisReadNetworkAddress**決定する値が範囲外です、永続的なメディア アクセス制御 (MAC) アドレスまたは既定のアドレスを代わりに使用してください。

## <a name="oid-specific-issues"></a>OID に固有の問題

- ミニポート ドライバーで、その[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)または[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数の場合は、任意のオブジェクト識別子を検証する必要があります設定 (OID) の値をドライバーが要求されました。 ドライバーは、設定する値が範囲外であるかを決定します、これはセットの要求が失敗します。 オブジェクト識別子の詳細については、[取得し、ミニポート ドライバー情報の設定と、WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)を参照してください。

- 場合、中間ドライバー *MiniportOidRequest*関数は、基になるミニポート ドライバーにセットの操作を渡さない、関数は、OID 値を検証する必要があります。 詳細については、[ドライバー クエリの中間と設定操作](intermediate-driver-query-and-set-operations.md)を参照してください。

### <a name="query-oid-security-guidelines"></a>クエリの OID のセキュリティ ガイドライン

ほとんどのクエリの Oid は、システム上の任意のユーザー モード アプリケーションで発行できます。 クエリの Oid を特定のガイドラインに従います。

1. 常に検証、バッファーのサイズが十分な大きさで出力します。 出力バッファー サイズ チェックなしのいずれかのクエリ OID ハンドラーは、セキュリティ バグです。

    ```c++
    if (oid->DATA.QUERY_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        oid->DATA.QUERY_INFORMATION.BytesNeeded = sizeof(ULONG);
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 常に正しいと最小値を BytesWritten に記述します。 赤いフラグを割り当てるには`oid->BytesWritten = oid->InformationBufferLength`次の例のようにします。

    ```c++
    // ALWAYS WRONG
    oid->DATA.QUERY_INFORMATION.BytesWritten = DATA.QUERY_INFORMATION.InformationBufferLength; 
    ```

    OS はユーザー モード アプリケーションに送り返さ BytesWritten バイトをコピーします。 最終的に可能性があります、OS BytesWritten が、ドライバーが実際に記述したバイト数よりも大きい場合のコピー初期化されていないユーザー モードでは、カーネル メモリ情報漏えいの脆弱性であります。 代わりに、次のようにコードを使用します。

    ```c++
    oid->DATA.QUERY_INFORMATION.BytesWritten = sizeof(ULONG);
    ``` 

3. バッファーから返された値を読み取ることはありません。 場合によっては、OID の出力バッファーは、悪意のあるユーザー モード プロセスに直接マップします。 記述した後、悪意のあるプロセスは、出力バッファーを変更できます。 たとえば、次のコードことができます、攻撃を受けるため、攻撃者が書き込まれる NumElements を変更できます。

    ```c++
    output->NumElements = 4;
    for (i = 0 ; i < output->NumElements ; i++) {
        output->Element[i] = . . .;
    }
    ```
    バッファーから読み取りを回避するには、ローカル コピーを保持します。 たとえば、上記の例を修正するには、新しいスタック変数を導入します。

    ```c++
    ULONG num = 4;
    output->NumElements = num;
    for (i = 0 ; i < num; i++) {
        output->Element[i] = . . .;
    }
    ```

    この方法で、ループは、ドライバーのスタック変数から返された読み取り`num`と、出力バッファーからではなく。 ドライバーもと出力バッファーとしてマークする必要があります、`volatile`をコンパイラが暗黙的にこの修正プログラムを元に戻すことを防ぐために、キーワード。

### <a name="set-oid-security-guidelines"></a>OID のセキュリティのガイドラインを設定します。

ほとんどの設定の Oid は、セキュリティ グループ管理者やシステムで実行されているユーザー モード アプリケーションで発行できます。 これらは一般的に信頼されたアプリケーションが、ミニポート ドライバーもする必要があります許可しないメモリの破損またはカーネル コードの挿入します。 Oid の設定をこれらの特定の規則に従います。

1.  常に検証、入力が十分な大きさです。 入力バッファーのサイズ チェックなしのいずれかの OID セット ハンドラーは、セキュリティの脆弱性を持ちます。

    ```c++
    if (oid->DATA.SET_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 埋め込みのオフセットで OID を検証するときに、埋め込まれたバッファーが、OID ペイロード内にあるを検証する必要があります。 これには、いくつかのチェックが必要です。 たとえば、 [OID_PM_ADD_WOL_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569764)チェックする必要がある埋め込みのパターンを提供することがあります。 適切な検証では、チェックが必要です。

    1. InformationBufferSize > sizeof(NDIS_PM_PACKET_PATTERN) を =

        ```c++
        PmPattern = (PNDIS_PM_PACKET_PATTERN) InformationBuffer;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN))
        {
            Status = NDIS_STATUS_BUFFER_TOO_SHORT;
            *BytesNeeded = sizeof(NDIS_PM_PACKET_PATTERN);
            break;
        }
        ```

    2. パターン PatternOffset]-> [+ パターン PatternSize]-> [オーバーフローできません

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternSize, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

        これら 2 つのチェックは、次の例のようなコードを使用して結合できます。

        ```c++
        ULONG TotalSize = 0;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN) ||
            !NT_SUCCESS(RtlUlongAdd(Pattern->PatternSize, Pattern->PatternOffset, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
    3. InformationBuffer + パターン PatternOffset]-> [+ パターン PatternLength]-> [オーバーフローできません

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            (!NT_SUCCESS(RtlUlongAdd(TotalSize, InformationBuffer, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

    4. パターン PatternOffset]-> [+ パターン PatternLength]-> [< InformationBufferSize を =

        ```c++
        ULONG TotalSize = 0;
        if(!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            TotalSize > InformationBufferLength)) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
### <a name="method-oid-security-guidelines"></a>メソッドの OID のセキュリティのガイドライン

メソッドの Oid は、セキュリティ グループ管理者やシステムで実行されているユーザー モード アプリケーションで発行できます。 セットと、クエリの組み合わせは、ガイダンスの両方の上記のリストは、メソッドの Oid にも適用されますので、です。

## <a name="other-network-driver-security-issues"></a>その他のネットワーク ドライバーのセキュリティの問題

- 多くの NDIS ミニポート ドライバーでは、NdisRegisterDeviceEx を使用して制御装置を公開します。 WDM ドライバーと同じすべてのセキュリティ規則では、IOCTL ハンドラー、これを監査する必要があります。 詳細については、[I/O 制御コードに関するセキュリティの問題](https://msdn.microsoft.com/library/windows/hardware/ff563700(v=vs.85).aspx)を参照してください。

- 適切に設計された NDIS ミニポート ドライバーは、特定のプロセスのコンテキストで呼び出される依存したり (Ioctl) 例外をされている Oid で usermode を非常に密接に対話する必要がありますしません。 Usermode ハンドルを開いたり、ユーザー モードの待機を実行したり usermode クォータに対してメモリを割り当てられているミニポートを表示する赤いフラグがあります。 そのコードを調査する必要があります。

- ほとんどの NDIS ミニポート ドライバーは、パケットのペイロードを解析中に含まれていない必要があります。 場合によっては、ただし、必要があります。 そのため、このコードは、ドライバーが、信頼できないソースからデータを解析中に、非常に慎重に監査してください場合。

- カーネル モードのメモリを割り当てるときに、標準は、NDIS ドライバー適切な使用する必要があります[プール オプトイン メカニズムに NX](https://docs.microsoft.com/windows-hardware/drivers/kernel/nx-pool-opt-in-mechanisms)します。 WDK 8 以降、`NdisAllocate*`ファミリの関数が正常に有効にします。

