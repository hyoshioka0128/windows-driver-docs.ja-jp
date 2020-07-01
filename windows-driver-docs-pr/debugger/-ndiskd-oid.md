---
title: ndiskd oid
description: Ndiskd oid 拡張機能には、NDIS OID 要求に関する情報が表示されます。
ms.assetid: FCDE2F78-98C0-4437-999A-4566FEB5D7BB
keywords:
- ndiskd oid Windows デバッグ
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.oid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c3538d2631ac3cf01c453bcdc23b6c6024a22566
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593892"
---
# <a name="ndiskdoid"></a>!ndiskd.oid

**! Ndiskd oid**拡張機能には、NDIS oid 要求に関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、すべてのミニポートとフィルターに対する保留中のすべての OID 要求の一覧が表示されます。 各ミニポートまたはフィルターには、1つの保留中の OID 要求と、任意の数のキューに置かれた OID 要求があります。

通常、フィルターは OID 要求を複製して、複製を渡すことに注意してください。 つまり、プロトコルが1つの OID 要求を発行する場合でも、複製された要求のインスタンスが複数存在する可能性があります。1つはフィルターごとに、もう1つはミニポートです。 **! ndiskd oid**によって各複製が個別に表示されるため、プロトコルが実際に発行した数よりも多くの保留中の oid が表示される場合があります。

```console
!ndiskd.oid [-handle <x>] [-legacyoid] [-nolimit>] [-miniport <x>] 
```

## <a name="parameters"></a>パラメーター

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
NDIS \_ OID 要求のハンドル \_

<span id="_______-legacyoid______"></span><span id="_______-LEGACYOID______"></span>*-legacyoid*   
は、NDIS OID 要求ではなく、レガシ NDIS 要求として扱わ \_ \_ \_ れます。

<span id="_______-nolimit______"></span><span id="_______-NOLIMIT______"></span>*-nolimit*   
では、表示される保留中の Oid の数は制限されません。

<span id="_______-miniport______"></span><span id="_______-MINIPORT______"></span>*-ミニポート*   
このミニポートのスタックで保留中の OID 要求を検索します。

### <a name="dll"></a>[DLL]

Ndiskd.dll

### <a name="remarks"></a>Remarks

**! ndiskd oid**は、システム上の保留中のすべての oid の一覧を一度に表示します。これにより、システムのハングや[0x9f バグチェック](bug-check-0x9f--driver-power-state-failure.md)の状況 (ドライバーの \_ 電源 \_ 状態の障害) のデバッグに役立ち \_ ます。 たとえば、架空の0x9F バグチェックを分析すると、システムが IRP でハングし、NDIS を待機していたことが判明したとします。 NDIS では、OS からの Irp は電源遷移を含む Oid に変換されるので、 **! ndiskd oid**を実行すると、スタックの一番下にあるデバイスが[oid \_ PNP \_ SET \_ パワー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)に clinging され、スタックの残りの部分がハングしている可能性があります。 NDIS ドライバーでは、OID を1秒以上保留しないようにする必要があります。そのため、デバイスの OID が長時間保留になっている原因を調査して、問題を解決することができます。

### <a name="examples"></a>例

正常に実行されているシステムで保留中の OID の例を確認するには、ミニポートの OID 要求ハンドラールーチンにブレークポイントを設定します (ミニポートの対応するミニポートドライバー)。 最初に、パラメーターを付けずに[**! ndiskd**](-ndiskd-minidriver.md)コマンドを実行して、システム上のミニポートドライバーの一覧を取得します。 この例の出力では、kdnic ミニドライバー、ffffdf801418d650. のハンドルを探します。

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

ミニドライバーのハンドルをクリックし、詳細ページの下部にある [ハンドラー] リンクをクリックして、そのハンドラーの一覧を表示します。 別の方法として、 **! ミニドライバー**コマンドを入力することもできます。 ミニドライバーのハンドラーの一覧が表示されたら、この例では、ハンドルが fffff80f1fd71c90 である OidRequestHandler を探します。

```console
2: kd> !ndiskd.minidriver ffffdf801418d650 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80f1fd78230  bp
    SetOptionsHandler                      fffff80f1fd72800  bp
    HaltHandlerEx                          fffff80f1fd78040  bp
    ShutdownHandlerEx                      fffff80f1fd722c0  bp

    CheckForHangHandlerEx                  fffff80f1fd72810  bp
    ResetHandlerEx                         fffff80f1fd72f70  bp

    PauseHandler                           fffff80f1fd78000  bp
    RestartHandler                         fffff80f1fd78940  bp

    OidRequestHandler                      fffff80f1fd71c90  bp
    CancelOidRequestHandler                fffff80f1fd722c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80f1fd789a0  bp

    SendNetBufferListsHandler              fffff80f1fd71870  bp
    ReturnNetBufferListsHandler            fffff80f1fd71b50  bp
    CancelSendHandler                      fffff80f1fd722c0  bp
```

次に、OidRequestHandler の右側にある "bp" リンクをクリックするか、または[**bp-handle**](bp--bu--bm--set-breakpoint-.md)コマンドにハンドルを入力して、そのルーチンにブレークポイントを設定します。 次に、 **g**コマンドを入力して、デバッグ対象ターゲットマシンの実行を許可し、設定したブレークポイントにヒットします。

```console
2: kd> bp fffff80f1fd71c90
2: kd> g
Breakpoint 1 hit
fffff80f`1fd71c90 448b4204        mov     r8d,dword ptr [rdx+4]
```

前の例で示したように、ミニドライバーの OID 要求ハンドラールーチンでブレークポイントをトリガーした後、! ndiskd OID コマンドを実行して、システム上のすべての保留中の Oid の一覧を表示できます。

```console
1: kd> !ndiskd.oid


ALL PENDING OIDs

    NetAdapter         ffffdf80140c71a0 - Microsoft Kernel Debug Network Adapter
        Current OID        OID_GEN_STATISTICS
    Filter             ffffdf8014950c70 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000
        Current OID        OID_GEN_STATISTICS
    Filter             ffffdf801494dc70 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
        Current OID        OID_GEN_STATISTICS
```

この例では、保留中の OID は[oid 生成 \_ \_ 統計](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)です。 ! Ndiskd oid の結果を見ると、フィルターによって OID 要求が複製され、スタックに渡されます。また、Oid は通常、フィルターによってミニポートにフィルター処理されます。 したがって、この例では、同じ名前を持つ3つの別個の OID 要求があるように見えるかもしれませんが、実際には、3つの Oid と3つのドライバーに物理的に分散された論理操作が1つあります。

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[0x9F バグチェック](bug-check-0x9f--driver-power-state-failure.md)

[OID \_ PNP \_ 設定の \_ 電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

[**bp、bu、bm (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)

[OID \_ 生成 \_ 統計](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)

[NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[NDIS OID 要求インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
