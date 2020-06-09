---
title: NDIS 拡張機能 (Ndiskd.dll)
description: NDIS 拡張機能 (Ndiskd.dll)
ms.assetid: bf4a7cc2-0116-4d6d-8a6f-2e9dc77d3631
keywords:
- NDIS 拡張機能 (ndiskd .dll)
- ndiskd .dll (NDIS 拡張機能)
- 拡張機能、NDIS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e26f38e7dda77987d0fa09d94654e53862d165d
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534775"
---
# <a name="ndis-extensions-ndiskddll"></a>NDIS 拡張機能 (Ndiskd.dll)


## <span id="ddk_ndis_extensions_ndiskd_dll__dbg"></span><span id="DDK_NDIS_EXTENSIONS_NDISKD_DLL__DBG"></span>


このセクションでは、で使用可能なコマンドについて説明します。 ndiskd は、NDIS (Network Device Interface Specification) ドライバーのデバッグに便利なデバッガー拡張機能です。 これらのコマンドを使用すると、ネットワークドライバーの開発者は、Windows ネットワークスタックのより大きな画像と、そのドライバーがどのように対話するかを確認できます。 With !ndiskd, you can see the state of all network adapters ([**!ndiskd.netadapter**](-ndiskd-netadapter.md)), a visual diagram of the computer's network stack ([**!ndiskd.netreport**](-ndiskd-netreport.md)), a log of traffic on the network adapters([**!ndiskd.nbllog**](-ndiskd-nbllog.md)), or a list of all pending OID requests ([**!ndiskd.oid**](-ndiskd-oid.md)).

これらのコマンドは、Ndiskd .dll にあります。 シンボルを読み込むには、デバッガーのコマンドウィンドウで「」と入力します **。** シンボルが正常に読み込まれたことを確認するには、 [**! lmi ndis**](-lmi.md)拡張機能を使用して、"シンボルが正常に読み込まれました" という語句を下部に検索します。 出力は次の例のようになります。

```dbgcmd
3: kd> !lmi ndis
Loaded Module Info: [ndis] 
         Module: ndis
   Base Address: fffff80e2e150000
     Image Name: ndis.sys
   Machine Type: 34404 (X64)
     Time Stamp: 57f4c58d Wed Oct  5 02:19:09 2016
           Size: 128000
       CheckSum: 1213f7
Characteristics: 22  
Debug Data Dirs: Type  Size     VA  Pointer
             CODEVIEW    21, 7b1b8,   79fb8 RSDS - GUID: {06A2E58C-996D-4419-81A0-BB293BD63BCA}
               Age: 1, Pdb: ndis.pdb
                   ??   880, 7b1dc,   79fdc [Data not mapped]
     Image Type: MEMORY   - Image read successfully from loaded memory.
    Symbol Type: PDB      - Symbols loaded successfully from image header.
                 c:\Debuggers\sym\ndis.pdb\06A2E58C996D441981A0BB293BD63BCA1\ndis.pdb
       Compiler: Linker - front end [0.0 bld 0] - back end [14.0 bld 23917]
    Load Report: private symbols & lines, source indexed 
                 c:\Debuggers\sym\ndis.pdb\06A2E58C996D441981A0BB293BD63BCA1\ndis.pdb
```

## <a name="span-id_ndiskd_hyperlinksspanspan-id_ndiskd_hyperlinksspanspan-id_ndiskd_hyperlinksspanndiskd-hyperlinks"></a><span id="_ndiskd_Hyperlinks"></span><span id="_ndiskd_hyperlinks"></span><span id="_NDISKD_HYPERLINKS"></span>! ndiskd ハイパーリンク


の拡張コマンドの多くは、デバッガーウィンドウに表示される結果にハイパーリンクがあることを示しています。 これらのハイパーリンクのテキストは、デバッグ対象マシンでコマンドを実行したときに表示される内容の正確な形式を示すために用意されているサンプルに残されています。 一部の例では、これらのリンクをクリックすることを明示的に参照しているため、一般的な使用フローを理解できます。ただし、各コマンドの代替コマンドライン形式も用意されています。

## <a name="span-idcommon_parametersspanspan-idcommon_parametersspanspan-idcommon_parametersspancommon-parameters"></a><span id="Common_Parameters"></span><span id="common_parameters"></span><span id="COMMON_PARAMETERS"></span>共通パラメーター


すべて! ndiskd コマンドでは、次のジェネリックパラメーターがサポートされています。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span>*-verbose*   
追加の詳細を表示します。

<span id="_______-terse______"></span><span id="_______-TERSE______"></span>*-簡潔*   
一部の定型の出力を抑制します。

<span id="_______-static______"></span><span id="_______-STATIC______"></span>*-static*   
一部の対話型出力を抑制します。

<span id="_______-dml_0_1______"></span><span id="_______-DML_0_1______"></span>*-dml 0 | 1*   
DML (デバッガーマークアップ言語) の出力を有効にするかどうかを制御します。

<span id="_______-unicode_0_1______"></span><span id="_______-UNICODE_0_1______"></span>*-unicode 0 | 1*   
Unicode 文字の出力を許可するかどうかを制御します。

<span id="_______-indent_N______"></span><span id="_______-indent_n______"></span><span id="_______-INDENT_N______"></span>*-インデント N*   
インデントのレベルごとに*N 個*のスペースを使用します。

<span id="_______-force______"></span><span id="_______-FORCE______"></span>*-force*   
リモートデータの整合性に関する一部の安全性チェックを上書きします。

<span id="_______-tracedata______"></span><span id="_______-TRACEDATA______"></span>*-tracedata*   
デバッグする詳細トレースメッセージを表示します。 ndiskd 自体。

## <a name="span-idnet_adapter__ndis_driver__and_general_commandsspanspan-idnet_adapter__ndis_driver__and_general_commandsspanspan-idnet_adapter__ndis_driver__and_general_commandsspannet-adapter-ndis-driver-and-general-commands"></a><span id="Net_Adapter__NDIS_Driver__and_General_Commands"></span><span id="net_adapter__ndis_driver__and_general_commands"></span><span id="NET_ADAPTER__NDIS_DRIVER__AND_GENERAL_COMMANDS"></span>Net アダプター、NDIS ドライバー、および一般的なコマンド


次のコマンドは、コンピューターのネットワークアダプター、ネットワークドライバー、およびネットワークスタックに関連付けられている一般的なコマンド (rcvqueues、開いているフィルター、Oid、および RW ロックなど) に関する情報を表示します。

-   [**!ndiskd.netadapter**](-ndiskd-netadapter.md)
-   [**!ndiskd.minidriver**](-ndiskd-minidriver.md)
-   [**!ndiskd.rcvqueue**](-ndiskd-rcvqueue.md)
-   [**!ndiskd.protocol**](-ndiskd-protocol.md)
-   [**!ndiskd.mopen**](-ndiskd-mopen.md)
-   [**!ndiskd.filter**](-ndiskd-filter.md)
-   [**!ndiskd.filterdriver**](-ndiskd-filterdriver.md)
-   [**!ndiskd.oid**](-ndiskd-oid.md)
-   [**!ndiskd.ndisrwlock**](-ndiskd-ndisrwlock.md)
-   [**!ndiskd.netreport**](-ndiskd-netreport.md)

## <a name="span-idnet_buffer_list_and_net_buffer_commandsspanspan-idnet_buffer_list_and_net_buffer_commandsspanspan-idnet_buffer_list_and_net_buffer_commandsspannet_buffer_list-and-net_buffer-commands"></a><span id="NET_BUFFER_LIST_and_NET_BUFFER_Commands"></span><span id="net_buffer_list_and_net_buffer_commands"></span><span id="NET_BUFFER_LIST_AND_NET_BUFFER_COMMANDS"></span>NET \_ バッファー \_ の一覧と Net \_ buffer コマンド


次のコマンドは、 [**net \_ buffer \_ LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)と[**net \_ buffer**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)構造体に関する情報を表示します。

-   [**!ndiskd.nbl**](-ndiskd-nbl.md)
-   [**!ndiskd.nb**](-ndiskd-nb.md)
-   [**!ndiskd.nblpool**](-ndiskd-nblpool.md)
-   [**!ndiskd.nbpool**](-ndiskd-nbpool.md)
-   [**!ndiskd.pendingnbls**](-ndiskd-pendingnbls.md)
-   [**!ndiskd.nbllog**](-ndiskd-nbllog.md)

## <a name="span-idnetadaptercx_commandsspanspan-idnetadaptercx_commandsspanspan-idnetadaptercx_commandsspannetadaptercx-commands"></a><span id="NetAdapterCx_Commands"></span><span id="netadaptercx_commands"></span><span id="NETADAPTERCX_COMMANDS"></span>NetAdapterCx コマンド


次のコマンドは、ネットワークアダプターの WDF Class Extension (NetAdapterCx) リンクが \[ 未定で、 \] 関連付けられている構造に関する情報を表示し \_ ます。また、net RING バッファーリンクを未定にし、 \_ \[ \] ネットパケット \_ リンク \[ \] を未定にします。

-   [**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)
-   [**!ndiskd.netqueue**](-ndiskd-netqueue.md)
-   [**!ndiskd.netrb**](-ndiskd-netrb.md)
-   [**!ndiskd.netpacket**](-ndiskd-netpacket.md)
-   [**!ndiskd.netpacketfragment**](-ndiskd-netpacketfragment.md)

## <a name="span-idnetwork_interface_commandsspanspan-idnetwork_interface_commandsspanspan-idnetwork_interface_commandsspannetwork-interface-commands"></a><span id="Network_Interface_Commands"></span><span id="network_interface_commands"></span><span id="NETWORK_INTERFACE_COMMANDS"></span>ネットワークインターフェイスのコマンド


次のコマンドは、ネットワークインターフェイスに関する情報を表示します。

-   [**!ndiskd.interfaces**](-ndiskd-interfaces.md)
-   [**!ndiskd.ifprovider**](-ndiskd-ifprovider.md)

## <a name="span-idndis_packet_commandsspanspan-idndis_packet_commandsspanspan-idndis_packet_commandsspanndis_packet-commands"></a><span id="NDIS_PACKET_Commands"></span><span id="ndis_packet_commands"></span><span id="NDIS_PACKET_COMMANDS"></span>NDIS \_ パケットコマンド


次のコマンドは、 [NDIS \_ パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造に関する情報を表示します。 これらの拡張機能は、従来の NDIS 5.x ドライバー用です。 NDIS \_ パケット構造とそれに関連付けられているアーキテクチャは非推奨となりました。

-   [**!ndiskd.pkt**](-ndiskd-pkt.md)
-   [**!ndiskd.pktpools**](-ndiskd-pktpools.md)
-   [**!ndiskd.findpacket**](-ndiskd-findpacket.md)

## <a name="span-idcondis_commandsspanspan-idcondis_commandsspanspan-idcondis_commandsspancondis-commands"></a><span id="CoNDIS_Commands"></span><span id="condis_commands"></span><span id="CONDIS_COMMANDS"></span>CoNDIS コマンド


次のコマンドは、[接続指向の NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)接続に関する情報を表示します。

-   [**!ndiskd.vc**](-ndiskd-vc.md)
-   [**!ndiskd.af**](-ndiskd-af.md)

## <a name="span-idndis_debugging_commandsspanspan-idndis_debugging_commandsspanspan-idndis_debugging_commandsspanndis-debugging-commands"></a><span id="NDIS_Debugging_Commands"></span><span id="ndis_debugging_commands"></span><span id="NDIS_DEBUGGING_COMMANDS"></span>NDIS デバッグコマンド


次のコマンドは、NDIS refcounts、イベントログ、スタックトレース、およびデバッグトレースに関する情報を表示します。

-   [**!ndiskd.ndisref**](-ndiskd-ndisref.md)
-   [**!ndiskd.ndisevent**](-ndiskd-ndisevent.md)
-   [**!ndiskd.ndisstack**](-ndiskd-ndisstack.md)
-   [**!ndiskd.dbglevel**](-ndiskd-dbglevel.md)
-   [**!ndiskd.dbgsystems**](-ndiskd-dbgsystems.md)

## <a name="span-idwdi_commandsspanspan-idwdi_commandsspanspan-idwdi_commandsspanwdi-commands"></a><span id="WDI_Commands"></span><span id="wdi_commands"></span><span id="WDI_COMMANDS"></span>WDI コマンド


次のコマンドは、 [WDI ミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)に関する情報を表示します。

-   [**!ndiskd.wdiadapter**](-ndiskd-wdiadapter.md)
-   [**!ndiskd.wdiminidriver**](-ndiskd-wdiminidriver.md)
-   [**!ndiskd.nwadapter**](-ndiskd-nwadapter.md)

## <a name="span-idndis_and__ndiskd_information_commandsspanspan-idndis_and__ndiskd_information_commandsspanspan-idndis_and__ndiskd_information_commandsspanndis-and-ndiskd-information-commands"></a><span id="NDIS_and__ndiskd_Information_Commands"></span><span id="ndis_and__ndiskd_information_commands"></span><span id="NDIS_AND__NDISKD_INFORMATION_COMMANDS"></span>NDIS および! ndiskd 情報コマンド


次のコマンドは、NDIS および ndiskd .dll に関する情報を表示します。

-   [**!ndiskd.ndis**](-ndiskd-ndis.md)
-   [**!ndiskd.ndiskdversion**](-ndiskd-ndiskdversion.md)

## <a name="span-idmiscellaneous_commandsspanspan-idmiscellaneous_commandsspanspan-idmiscellaneous_commandsspanmiscellaneous-commands"></a><span id="Miscellaneous_Commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>その他のコマンド


-   [**!ndiskd.ifstacktable**](-ndiskd-ifstacktable.md)
-   [**!ndiskd.compartments**](-ndiskd-compartments.md)
-   [**!ndiskd.ndisslot**](-ndiskd-ndisslot.md)

## <a name="span-idrelated_topicsspanspan-idrelated_topicsspanspan-idrelated_topicsspanrelated-topics"></a><span id="Related_Topics"></span><span id="related_topics"></span><span id="RELATED_TOPICS"></span>関連項目


Windows Vista 以降の NDIS ドライバーの設計の詳細については、「[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)」を参照してください。

Windows Vista 以降の NDIS ドライバーのリファレンスの詳細については、「 [Windows vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

! Ndiskd デバッガーコマンドを使用してネットワークスタックをデバッグする方法の例については、「[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)」を参照してください。

 

 






