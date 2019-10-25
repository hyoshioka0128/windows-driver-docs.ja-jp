---
title: ミニドライバー、ミニポート ドライバー、ドライバー ペア
description: ミニドライバーまたはミニポート ドライバーは、ドライバー ペアの片方として機能します。
ms.assetid: 33387A72-5278-4637-AED4-C010E4C1616B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19cf08d6a8ce1a7d2f81ee5907cdc664a7f004b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825166"
---
# <a name="minidrivers-miniport-drivers-and-driver-pairs"></a>ミニドライバー、ミニポート ドライバー、ドライバー ペア


ミニドライバーまたはミニポート ドライバーは、ドライバー ペアの片方として機能します。 (ミニポート、ポート) のようなドライバー ペアを使うと、ドライバー開発が容易になります。 ドライバー ペアでは、一方のドライバーがデバイスの集まり全体に共通する一般的なタスクを処理し、もう一方のドライバーが個々のデバイスに固有のタスクを担当します。 デバイス固有のタスクを処理するドライバーは、ミニポート ドライバー、ミニクラス ドライバー、ミニドライバーなど、さまざまな名称で呼ばれています。

Microsoft は、汎用的なドライバーを提供し、通常、個々のハードウェア ベンダーが固有のドライバーを提供します。 このトピックを読む前にまず、「[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)」と「[I/O 要求パケット](i-o-request-packets.md)」で説明する概念について理解しておく必要があります。

個々のカーネル モード ドライバーでは、[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) という名前の関数が実装されている必要があります。この関数は、ドライバーが読み込まれた直後に呼び出されます。 **DriverEntry** 関数により、[**DRIVER\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 構造体に含まれる特定のメンバーには、当該のドライバーがこれ以外に実装するいくつかの関数へのポインターが提供されます。 たとえば **DriverEntry** 関数は、次の図に示すように、**DRIVER\_OBJECT** 構造体の **Unload** メンバーに、ドライバーの [*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 関数へのポインターを提供します。

![DRIVER\-OBJECT 構造体と Unload メンバーの図](images/driverfunctionpointers02.png)

次の図のように、[**DRIVER\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 構造体の **MajorFunction** メンバーは、I/O 要求パケット ([**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)) を処理する関数に対するポインターの配列になっています。 通常、ドライバーは **MajorFunction** 配列に含まれるいくつかのメンバーに対し、各種の IRP を処理する関数 (ドライバーで実装される) へのポインターを提供します。

![DRIVER\-OBJECT 構造体と MajorFunction メンバーの図](images/driverfunctionpointers03.png)

IRP は、**IRP\_MJ\_READ**、**IRP\_MJ\_WRITE**、**IRP\_MJ\_PNP** のような定数で識別されるメジャー関数コードに応じて分類することができます。 メジャー関数コードを識別する定数は、**MajorFunction** 配列のインデックスとしての役割を果たします。 たとえば、**IRP\_MJ\_WRITE** というメジャー関数コードを含む IRP を処理するディスパッチ関数を実装するドライバーを考えてみます。 この場合、ドライバーは、配列の **MajorFunction**\[IRP\_MJ\_WRITE\] 要素にディスパッチ関数へのポインターを提供する必要があります。

通常、ドライバーは **MajorFunction** 配列に含まれるいくつかの要素にポインターを提供し、残りの要素については、I/O マネージャーから指定される既定値を設定します。 次の例は、[ **!drvobj**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-drvobj) デバッガー拡張機能を使って、parport ドライバーが提供する関数ポインターを調べる方法を示したものです。

``` syntax
0: kd> !drvobj parport 2
Driver object (fffffa80048d9e70) is for:
 \Driver\Parport
DriverEntry:   fffff880065ea070 parport!GsDriverEntry
DriverStartIo: 00000000 
DriverUnload:  fffff880065e131c parport!PptUnload
AddDevice:     fffff880065d2008 parport!P5AddDevice

Dispatch routines:
[00] IRP_MJ_CREATE                      fffff880065d49d0    parport!PptDispatchCreateOpen
[01] IRP_MJ_CREATE_NAMED_PIPE           fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[02] IRP_MJ_CLOSE                       fffff880065d4a78    parport!PptDispatchClose
[03] IRP_MJ_READ                        fffff880065d4bac    parport!PptDispatchRead
[04] IRP_MJ_WRITE                       fffff880065d4bac    parport!PptDispatchRead
[05] IRP_MJ_QUERY_INFORMATION           fffff880065d4c40    parport!PptDispatchQueryInformation
[06] IRP_MJ_SET_INFORMATION             fffff880065d4ce4    parport!PptDispatchSetInformation
[07] IRP_MJ_QUERY_EA                    fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[08] IRP_MJ_SET_EA                      fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[09] IRP_MJ_FLUSH_BUFFERS               fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0c] IRP_MJ_DIRECTORY_CONTROL           fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0e] IRP_MJ_DEVICE_CONTROL              fffff880065d4be8    parport!PptDispatchDeviceControl
[0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff880065d4c24    parport!PptDispatchInternalDeviceControl
[10] IRP_MJ_SHUTDOWN                    fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[11] IRP_MJ_LOCK_CONTROL                fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[12] IRP_MJ_CLEANUP                     fffff880065d4af4    parport!PptDispatchCleanup
[13] IRP_MJ_CREATE_MAILSLOT             fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[14] IRP_MJ_QUERY_SECURITY              fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[15] IRP_MJ_SET_SECURITY                fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[16] IRP_MJ_POWER                       fffff880065d491c    parport!PptDispatchPower
[17] IRP_MJ_SYSTEM_CONTROL              fffff880065d4d4c    parport!PptDispatchSystemControl
[18] IRP_MJ_DEVICE_CHANGE               fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[19] IRP_MJ_QUERY_QUOTA                 fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[1a] IRP_MJ_SET_QUOTA                   fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[1b] IRP_MJ_PNP                         fffff880065d4840    parport!PptDispatchPnp
```

デバッガー出力を見ると、parport.sys により、ドライバーに対するエントリ ポイントとして **GsDriverEntry** が実装されているのがわかります。 **GsDriverEntry** は、ドライバーのビルド時に自動的に生成されます。この関数は、一部の初期化を行い、ドライバーの開発者によって実装された [**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) を呼び出します。

また、parport ドライバー (その [**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 関数中) により、以下のメジャー関数コードに対し、ディスパッチ関数へのポインターが提供されていることがわかります。

-   IRP\_MJ\_CREATE
-   IRP\_MJ\_CLOSE
-   IRP\_MJ\_READ
-   IRP\_MJ\_WRITE
-   IRP\_MJ\_QUERY\_INFORMATION
-   IRP\_MJ\_SET\_INFORMATION
-   IRP\_MJ\_DEVICE\_CONTROL
-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL
-   IRP\_MJ\_CLEANUP
-   IRP\_MJ\_POWER
-   IRP\_MJ\_SYSTEM\_CONTROL
-   IRP\_MJ\_PNP

**MajorFunction** 配列の残りの要素には、既定のディスパッチ関数 **nt!IopInvalidDeviceRequest** に対するポインターが保持されます。

デバッガー出力を見ると、parport ドライバーでは [*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) と [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) に関数のポインターが提供されていますが、[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) には関数のポインターが提供されていないことがわかります。 *AddDevice* は、その関数ポインターが [**DRIVER\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 構造体に格納されていないという意味で、特殊な関数です。 関数ポインターは、**DRIVER\_OBJECT** 構造体の拡張機能に含まれる **AddDevice** メンバーに格納されています。 次の図は、[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 関数の中で parport ドライバーが提供する各関数ポインターを示したものです。 parport が提供する関数ポインターには影が付けてあります。

![DRIVER\-OBJECT 構造体の中の関数ポインターの図](images/driverfunctionpointers01.png)

## <a name="span-idmaking_it_easier_by_using_driver_pairsspanspan-idmaking_it_easier_by_using_driver_pairsspanspan-idmaking_it_easier_by_using_driver_pairsspanmaking-it-easier-by-using-driver-pairs"></a><span id="Making_it_easier_by_using_driver_pairs"></span><span id="making_it_easier_by_using_driver_pairs"></span><span id="MAKING_IT_EASIER_BY_USING_DRIVER_PAIRS"></span>ドライバー ペアによる作業の効率化


Microsoft の社の内外を問わず、ドライバー開発者が Windows Driver Model (WDM) にかかわる経験を重ねるに従い、ディスパッチ関数について次のような特徴が明らかになってきました。

-   ディスパッチ関数の相当部分がスケルトン コードで構成されています。 たとえば、関数コード IRP\_MJ\_PNP のディスパッチ関数の大部分がすべてのドライバーに共通しています。 ハードウェアの個々の部分を制御する個別のドライバーに限定されるのは、プラグ アンド プレイ (PnP) コードの一部だけです。
-   ディスパッチ関数は複雑で、正確に理解することが困難です。 スレッド同期、IRP キュー、IRP の取り消しなどの機能を実装するには、オペレーティング システムの動作について詳しい知識が必要になります。

Microsoft では、ドライバー開発者がこうした作業を容易に行うことができるように、テクノロジ固有のドライバー モデルをいくつか考案しました。 各テクノロジ固有のモデルは一見、それぞれ異なっているように思われますが、詳しく見てみると、その多くが次の共通のパラダイムに基づいていることがわかります。

-   ドライバーは、汎用的な処理を行う部分と特定のデバイスに固有の処理を行う部分の 2 つに分けられます。
-   汎用的な部分は Microsoft が作ります。
-   固有の部分は、Microsoft または個々のハードウェア ベンダーが作ります。

たとえば、Proseware と Contoso の両社が WDM ドライバーを使うおもちゃのロボットを製造していると仮定します。 Microsoft では、GeneralRobot.sys という汎用ロボット ドライバーを提供しているとします。 Proseware と Contoso はいずれも、独自のロボットの要件に対応した小規模のドライバーを作ることができます。 たとえば、Proseware では ProsewareRobot.sys というドライバーを作れば、ドライバー ペア (ProsewareRobot.sys と GeneralRobot.sys) として組み合わせることにより、単一の WDM ドライバーを形成することができます。 同様に、ContosoRobot.sys と GeneralRobot.sys のドライバー ペアにより、単一の WDM ドライバーを構成できます。 最も基本的な形式として、specific.sys と general.sys (固有ドライバーと汎用ドライバー) というペアを使うことにより、ドライバーを作ることができるということです。

## <a name="span-idfunction_pointers_in_driver_pairsspanspan-idfunction_pointers_in_driver_pairsspanspan-idfunction_pointers_in_driver_pairsspanfunction-pointers-in-driver-pairs"></a><span id="Function_pointers_in_driver_pairs"></span><span id="function_pointers_in_driver_pairs"></span><span id="FUNCTION_POINTERS_IN_DRIVER_PAIRS"></span>ドライバー ペア中の関数ポインター


specific.sys と general.sys のペアでは、Windows は specific.sys を読み込み、[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 関数を呼び出します。 specific.sys の **DriverEntry** 関数は、[**DRIVER\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 構造体に対するポインターを受け取ります。 通常、**DriverEntry** からは **MajorFunction** 配列に含まれるいくつかの要素に対して、ディスパッチ関数へのポインターが提供されることを期待します。 また、**DriverEntry** についても **DRIVER\_OBJECT** 構造体に含まれる **Unload** メンバー (および **StartIo** メンバー) とドライバー オブジェクトの拡張機能に含まれる **AddDevice** メンバーにポインターが提供されることを期待します。 ところがドライバー ペア モデルの場合、**DriverEntry** は必ずしもこのようには動作しません。 つまり specific.sys の **DriverEntry** 関数は、general.sys で実装された初期化関数に対し、**DRIVER\_OBJECT** 構造体を受け渡します。 次のコード例は、初期化関数を ProsewareRobot.sys と GeneralRobot.sys のペア中でどのように呼び出すことができるかを示したものです。

```ManagedCPlusPlus
PVOID g_ProsewareRobottCallbacks[3] = {DeviceControlCallback, PnpCallback, PowerCallback};

// DriverEntry function in ProsewareRobot.sys
NTSTATUS DriverEntry (DRIVER_OBJECT *DriverObject, PUNICODE_STRING RegistryPath)
{
   // Call the initialization function implemented by GeneralRobot.sys.
   return GeneralRobotInit(DriverObject, RegistryPath, g_ProsewareRobottCallbacks);
}
```

GeneralRobot.sys の初期化関数により、[**DRIVER\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 構造体 (およびその拡張機能) に含まれる該当メンバーと、**MajorFunction** 配列で該当する要素に対して関数ポインターが書き込まれます。 つまり I/O マネージャーからドライバー ペアに IRP が送られると、IRP はまず GeneralRobot.sys で実装されたディスパッチ関数に送られるということです。 GeneralRobot.sys が自力で IRP を処理できる場合は、固有ドライバー、ProsewareRobot.sys を使う必要はありません。 また GeneralRobot.sys が IRP の全部ではなく一部だけ処理できる場合は、ProsewareRobot.sys で実装されたいずれかのコールバック関数からの支援を利用します。 GeneralRobot.sys は、GeneralRobotInit の呼び出しの中で ProsewareRobot コールバックへのポインターを受け取ります。

[  **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) に戻ってからある時点で、Proseware Robot デバイス ノードに対するデバイス スタックが作られます。 デバイス スタックは次のようになります。

![Proseware Robot デバイス ノードの図 (デバイス スタックに AfterThought.sys (Filter DO)、ProsewareRobot.sys と GeneralRobot.sys (FDO)、および Pci.sys (PDO) という 3 つのデバイス オブジェクトがある状態)](images/driverpairs01.png)

上の図のように、Proseware Robot のデバイス スタックには 3 つのデバイス オブジェクトがあります。 一番上のデバイス オブジェクトはフィルター デバイス オブジェクト (Filter DO) で、フィルター ドライバー AfterThought.sys に関連付けられています。 中央のデバイス オブジェクトはファンクショナル デバイス オブジェクト (FDO) で、ドライバー ペア (ProsewareRobot.sys、GeneralRobot.sys) に関連付けられています。 ドライバー ペアは、デバイス スタックのファンクション ドライバーとして機能します。 一番下のデバイス オブジェクトは物理デバイス オブジェクト (PDO) で、Pci.sys に関連付けられています。

ドライバー ペアがデバイス スタックで占有するのは 1 レベルだけで、関連付けられるデバイス オブジェクトも FDO だけであることがわかります。 GeneralRobot.sys が IRP を処理するときに ProsewareRobot.sys に支援を要求することもありますが、これは、デバイス スタックに要求を渡すこととは異なります。 ドライバー ペアは単一の WDM ドライバーを形成して、これがデバイス スタック中で 1 レベルを占有します。 ドライバー ペアは、IRP を自力で処理するか、デバイス スタック上で Pci.sys に関連付けられた PDO に IRP を受け渡します。

## <a name="span-idexample_of_a_driver_pairspanspan-idexample_of_a_driver_pairspanspan-idexample_of_a_driver_pairspanexample-of-a-driver-pair"></a><span id="Example_of_a_driver_pair"></span><span id="example_of_a_driver_pair"></span><span id="EXAMPLE_OF_A_DRIVER_PAIR"></span>ドライバー ペアの例


たとえば、ワイヤレス ネットワーク カードを搭載したノート PC で、デバイス マネージャーにより、ネットワーク カードのドライバーとして netwlv64.sys が特定されたと仮定します。 [  **!drvobj**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-drvobj) デバッガー拡張機能を使って、netwlv64.sys の関数ポインターを調べることができます。

``` syntax
1: kd> !drvobj netwlv64 2
Driver object (fffffa8002e5f420) is for:
 \Driver\netwlv64
DriverEntry:   fffff8800482f064 netwlv64!GsDriverEntry
DriverStartIo: 00000000 
DriverUnload:  fffff8800195c5f4 ndis!ndisMUnloadEx
AddDevice:     fffff88001940d30 ndis!ndisPnPAddDevice
Dispatch routines:
[00] IRP_MJ_CREATE                      fffff880018b5530 ndis!ndisCreateIrpHandler
[01] IRP_MJ_CREATE_NAMED_PIPE           fffff88001936f00 ndis!ndisDummyIrpHandler
[02] IRP_MJ_CLOSE                       fffff880018b5870 ndis!ndisCloseIrpHandler
[03] IRP_MJ_READ                        fffff88001936f00 ndis!ndisDummyIrpHandler
[04] IRP_MJ_WRITE                       fffff88001936f00 ndis!ndisDummyIrpHandler
[05] IRP_MJ_QUERY_INFORMATION           fffff88001936f00 ndis!ndisDummyIrpHandler
[06] IRP_MJ_SET_INFORMATION             fffff88001936f00 ndis!ndisDummyIrpHandler
[07] IRP_MJ_QUERY_EA                    fffff88001936f00 ndis!ndisDummyIrpHandler
[08] IRP_MJ_SET_EA                      fffff88001936f00 ndis!ndisDummyIrpHandler
[09] IRP_MJ_FLUSH_BUFFERS               fffff88001936f00 ndis!ndisDummyIrpHandler
[0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff88001936f00 ndis!ndisDummyIrpHandler
[0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff88001936f00 ndis!ndisDummyIrpHandler
[0c] IRP_MJ_DIRECTORY_CONTROL           fffff88001936f00 ndis!ndisDummyIrpHandler
[0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff88001936f00 ndis!ndisDummyIrpHandler
[0e] IRP_MJ_DEVICE_CONTROL              fffff8800193696c ndis!ndisDeviceControlIrpHandler
[0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff880018f9114 ndis!ndisDeviceInternalIrpDispatch
[10] IRP_MJ_SHUTDOWN                    fffff88001936f00 ndis!ndisDummyIrpHandler
[11] IRP_MJ_LOCK_CONTROL                fffff88001936f00 ndis!ndisDummyIrpHandler
[12] IRP_MJ_CLEANUP                     fffff88001936f00 ndis!ndisDummyIrpHandler
[13] IRP_MJ_CREATE_MAILSLOT             fffff88001936f00 ndis!ndisDummyIrpHandler
[14] IRP_MJ_QUERY_SECURITY              fffff88001936f00 ndis!ndisDummyIrpHandler
[15] IRP_MJ_SET_SECURITY                fffff88001936f00 ndis!ndisDummyIrpHandler
[16] IRP_MJ_POWER                       fffff880018c35e8 ndis!ndisPowerDispatch
[17] IRP_MJ_SYSTEM_CONTROL              fffff880019392c8 ndis!ndisWMIDispatch
[18] IRP_MJ_DEVICE_CHANGE               fffff88001936f00 ndis!ndisDummyIrpHandler
[19] IRP_MJ_QUERY_QUOTA                 fffff88001936f00 ndis!ndisDummyIrpHandler
[1a] IRP_MJ_SET_QUOTA                   fffff88001936f00 ndis!ndisDummyIrpHandler
[1b] IRP_MJ_PNP                         fffff8800193e518 ndis!ndisPnPDispatch
```

デバッガー出力を見ると、netwlv64.sys により、ドライバーに対するエントリ ポイントとして、**GsDriverEntry** が実装されているのがわかります。 **GsDriverEntry** は、ドライバーのビルド時に自動的に生成されます。この関数は、一部の初期化を行い、ドライバーの開発者によって作られた [**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) を呼び出します。

この例では、[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) は netwlv64.sys により実装されますが、[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)、およびいくつかのディスパッチ関数は ndis.sys により実装されます。 netwlv64.sys は NDIS ミニポート ドライバー、ndis.sys は NDIS ライブラリと呼ばれます。 2 つのモジュールを組み合わせて、1 つのペア (NDIS ミニポート、NDIS ライブラリ) が形成されます。

下の図は、ワイヤレス ネットワーク カードのデバイス スタックを示します。 ドライバー ペア (netwlv64.sys と ndis.sys) がデバイス スタックで占有するのは 1 レベルだけで、関連付けられるデバイス オブジェクトも FDO だけであることがわかります。

![ワイヤレス ネットワーク カードのデバイス スタックの図 (FDO に関連付けられたドライバー ペアとして netwlv64.sys と ndis.sys、および PDO に関連付けられた Pci.sys) ](images/driverpairs02a.png)

## <a name="span-idavailable_driver_pairsspanspan-idavailable_driver_pairsspanspan-idavailable_driver_pairsspanavailable-driver-pairs"></a><span id="Available_driver_pairs"></span><span id="available_driver_pairs"></span><span id="AVAILABLE_DRIVER_PAIRS"></span>利用可能なドライバー ペア


各種のテクノロジ固有のドライバー モデルで、ドライバー ペアの固有部分と汎用部分に対してさまざまな名前が使われます。 多くの場合、ペアの固有部分には "ミニ" というプレフィックスが付きます。 以下に、利用可能なペア (固有ドライバー、汎用ドライバー) の一部を示します。

-   (ディスプレイ ミニポート ドライバー、ディスプレイ ポート ドライバー)
-   (オーディオ ミニポート ドライバー、オーディオ ポート ドライバー)
-   (ストレージ ミニポート ドライバー、ストレージ ポート ドライバー)
-   (バッテリ ミニクラス ドライバー、バッテリ クラス ドライバー)
-   (HID ミニドライバー、HID クラス ドライバー)
-   (チェンジャー ミニクラス ドライバー、チェンジャー ポート ドライバー)
-   (NDIS ミニポート ドライバー、NDIS ライブラリ)

**注**  一覧からわかるように、モデルの一部ではドライバー ペアの汎用部分について "*クラス ドライバー*" という用語が使われています。 この種のクラス ドライバーは、スタンドアロンのクラス ドライバーやクラス フィルター ドライバーとは異なります。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[すべてのドライバー開発者のための概念](concepts-and-knowledge-for-all-driver-developers.md)

[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)

[ドライバー スタック](driver-stacks.md)

 

 






