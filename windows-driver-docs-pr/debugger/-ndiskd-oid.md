---
title: ndiskd.oid
description: Ndiskd.oid 拡張機能には、NDIS OID 要求に関する情報が表示されます。
ms.assetid: FCDE2F78-98C0-4437-999A-4566FEB5D7BB
keywords:
- デバッグ ndiskd.oid Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.oid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d13728dd646a86dd7bd32073a0886142beb6c77
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238593"
---
# <a name="ndiskdoid"></a>!ndiskd.oid


**! Ndiskd.oid**拡張機能には、NDIS OID 要求に関する情報が表示されます。 パラメーターなしで、この拡張機能を実行する場合です。 すべてのミニポートおよびフィルターに ndiskd で OID 要求の保留中のすべての一覧が表示されます。 各ミニポートまたはフィルターは、最大で 1 つ保留 OID 要求と任意の数のキューに置かれた OID 要求を持っています。

フィルターが通常 OID 要求を複製し、の複製を渡すことに注意してください。 場合でも、プロトコルが 1 つの OID 要求を発行する場合があります複製要求の複数のインスタンスつまり:、各フィルターおよびミニポート内の別の 1 つ。 **! ndiskd.oid**保留中の複数の Oid プロトコルが実際に発行よりもが生じるため、個別に各クローンが表示されます。

```console
!ndiskd.oid [-handle <x>] [-legacyoid] [-nolimit>] [-miniport <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
ハンドルは、NDIS の\_OID\_要求

<span id="_______-legacyoid______"></span><span id="_______-LEGACYOID______"></span> *-legacyoid*   
従来の NDIS として扱います\_、NDIS ではなく要求\_OID\_を要求します。

<span id="_______-nolimit______"></span><span id="_______-NOLIMIT______"></span> *-nolimit*   
表示されている Oid 保留中の数は制限されません。

<span id="_______-miniport______"></span><span id="_______-MINIPORT______"></span> *-miniport*   
保留中のこのミニポートのスタックに OID 要求を検索します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

**! ndiskd.oid**リストが表示保留中のすべての Oid のシステムで一度にシステム ハングのデバッグできるようにまたは[0x9F バグ チェック](https://msdn.microsoft.com/library/windows/hardware/ff559329)状況 (ドライバー\_POWER\_状態\_エラー)。 たとえば、架空の 0x9F バグ チェックが明らかに、システムが IRP のハング状態にして、NDIS を待機していたことを分析します。 は、NDIS、OS から Irp が電源切り替え効果も含めて、Oid に変換を実行してその **! ndiskd.oid** 、この例で、スタックの一番下にあるデバイス可能性がありますがされて音を参照してくださいでした、 [OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)スタックの残りの部分がハングしたとします。 問題を解決するため、そのデバイスが長時間保留中の OID を保持する理由を調査する可能性がありますし、NDIS ドライバーは 1 秒間に複数の OID を保留しないを必要があります。

<a name="examples"></a>例
--------

正常に実行するシステムで保留中の OID の例を確認するには、(ミニポートの対応するミニポート ドライバーでは) でミニポートの OID 要求ハンドラー ルーチンにブレークポイントを設定します。 最初に、実行、 [ **! ndiskd.minidriver** ](-ndiskd-minidriver.md)システム上のミニポート ドライバーの一覧を取得するパラメーターなしでコマンド。 この例の出力には、kdnic ミニドライバー、ffffdf801418d650 のハンドルを探します.

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

ミニドライバーのハンドルをクリックし、そのハンドラーの一覧を表示するには、その詳細ページの下部にある「ハンドラー」リンクをクリックします。 別の方法として入力することができます、 **! ndiskd.minidriver-処理 - ハンドラー**コマンド。 ミニドライバーのハンドラーの一覧にした後は、そのハンドルはこの例では fffff80f1fd71c90、OidRequestHandler を探します。

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

または"bp"、OidRequestHandler の右側へのリンクを入力でクリックするか、これで、 [ **bp-処理**](bp--bu--bm--set-breakpoint-.md)ルーチンにブレークポイントを設定するには、そのハンドルを持つコマンド。 次に、入力、 **g**設定する対象コンピューターを実行し、ブレークポイントにヒットしますが、デバッグ対象を許可するコマンド。

```console
2: kd> bp fffff80f1fd71c90
2: kd> g
Breakpoint 1 hit
fffff80f`1fd71c90 448b4204        mov     r8d,dword ptr [rdx+4]
```

実行することができます、前の例に示すように、ミニドライバーの OID 要求ハンドラー ルーチンのブレークポイントがトリガーされるが、!、システムで保留中のすべての Oid の一覧を表示する ndiskd.oid コマンド。

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

この例では保留中の OID は[OID\_GEN\_統計](https://msdn.microsoft.com/library/windows/hardware/ff569640)します。 結果を表示する! ndiskd.oid、Oid 通常に渡されたフィルターからミニポートとフィルターは、OID 要求を複製し、下位のスタックでは、それらを渡すことを思い出してください。 そのため、この例では同じ名前の 3 つの独立した OID 要求があるように思えるかもしれませんは行われている 3 つの Oid と 3 つのドライバーに物理的に分散 1 論理操作実際にです。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[0x9F バグ チェック](https://msdn.microsoft.com/library/windows/hardware/ff559329)

[OID\_PNP\_設定\_電源](https://msdn.microsoft.com/library/windows/hardware/ff569780)

[**bp、bu、bm (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)

[OID\_GEN\_統計情報](https://msdn.microsoft.com/library/windows/hardware/ff569640)

[NDIS Oid](https://msdn.microsoft.com/library/windows/hardware/ff566707)

[NDIS OID 要求インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff566713)

 

 






