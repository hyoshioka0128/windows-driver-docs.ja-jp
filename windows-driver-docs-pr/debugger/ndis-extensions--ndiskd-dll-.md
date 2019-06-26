---
title: NDIS 拡張機能 (Ndiskd.dll)
description: NDIS 拡張機能 (Ndiskd.dll)
ms.assetid: bf4a7cc2-0116-4d6d-8a6f-2e9dc77d3631
keywords:
- NDIS 拡張機能 (ndiskd.dll)
- ndiskd.dll (NDIS 拡張)
- 拡張機能、NDIS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70b8ff4added860de71ced21c2e63ec9de2fcb77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366464"
---
# <a name="ndis-extensions-ndiskddll"></a>NDIS 拡張機能 (Ndiskd.dll)


## <span id="ddk_ndis_extensions_ndiskd_dll__dbg"></span><span id="DDK_NDIS_EXTENSIONS_NDISKD_DLL__DBG"></span>


このセクションで使用できるコマンドを説明します。 ndiskd、NDIS (Network Device Interface Specification) ドライバーのデバッグに役立つデバッガー拡張機能。 これらのコマンドでは、ネットワーク ドライバー開発者はネットワーク スタックと対話する方法、ドライバーが Windows の全体像を参照してください。 有効にします。 ! Ndiskd、すべてのネットワーク アダプターの状態を確認できます ([ **! ndiskd.netadapter**](-ndiskd-netadapter.md))、コンピューターのネットワーク スタックのビジュアル ダイアグラム ([ **! ndiskd.netreport**](-ndiskd-netreport.md))、ネットワーク アダプター上のトラフィックのログ ([ **! ndiskd.nbllog**](-ndiskd-nbllog.md))、または OID 要求の保留中のすべてのリスト ([ **! ndiskd.oid**](-ndiskd-oid.md)).

コマンドは、Ndiskd.dll で確認できます。 シンボルを読み込むには、次のように入力します。 **.reload/f ndis.sys**デバッガー コマンド ウィンドウにします。 シンボルが正常に読み込まれたことを確認するを使用して、 [ **! lmi ndis** ](-lmi.md)拡張機能と語句の「シンボルを正常に読み込む」下部の方に参照してください。 出力の次の例によう必要があります。

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

## <a name="span-idndiskdhyperlinksspanspan-idndiskdhyperlinksspanspan-idndiskdhyperlinksspanndiskd-hyperlinks"></a><span id="_ndiskd_Hyperlinks"></span><span id="_ndiskd_hyperlinks"></span><span id="_NDISKD_HYPERLINKS"></span>! ndiskd ハイパーリンク


コマンドでは、拡張機能の多くは! ndiskd デバッガー ウィンドウに表示される結果内のハイパーリンクが表示されます。 これらのハイパーリンクのテキストがデバッグ対象コンピューターに、コマンドを実行すると表示がされる内容の正確な形式を説明するために提供されるサンプルのままです。 一部の例も明示的に参照の例は、各コマンドのコマンドラインの代替フォームも提供する場合、一般的な使用フローを理解できるようにこれらのリンクをクリックします。

## <a name="span-idcommonparametersspanspan-idcommonparametersspanspan-idcommonparametersspancommon-parameters"></a><span id="Common_Parameters"></span><span id="common_parameters"></span><span id="COMMON_PARAMETERS"></span>共通パラメーター


すべて! ndiskd コマンドは、次のジェネリック パラメーターをサポートします。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span> *-verbose*   
追加の詳細を示します。

<span id="_______-terse______"></span><span id="_______-TERSE______"></span> *-terse*   
一部の定型コードの出力を抑制します。

<span id="_______-static______"></span><span id="_______-STATIC______"></span> *-静的*   
対話型の出力を抑制します。

<span id="_______-dml_0_1______"></span><span id="_______-DML_0_1______"></span> *dml 0 | 1*   
DML (デバッガーのマークアップ言語) の出力が有効になっているかどうかを制御します。

<span id="_______-unicode_0_1______"></span><span id="_______-UNICODE_0_1______"></span> *unicode 0 | 1*   
Unicode 文字の出力が許可されているかどうかを制御します。

<span id="_______-indent_N______"></span><span id="_______-indent_n______"></span><span id="_______-INDENT_N______"></span> *-N のインデント*   
使用して*N*インデントを 1 つの空白文字。

<span id="_______-force______"></span><span id="_______-FORCE______"></span> *-force*   
リモート データのサニティのいくつかの安全性チェックをオーバーライドします。

<span id="_______-tracedata______"></span><span id="_______-TRACEDATA______"></span> *-tracedata*   
デバッグの詳細トレース メッセージが表示されます。 ndiskd 自体。

## <a name="span-idnetadapterndisdriverandgeneralcommandsspanspan-idnetadapterndisdriverandgeneralcommandsspanspan-idnetadapterndisdriverandgeneralcommandsspannet-adapter-ndis-driver-and-general-commands"></a><span id="Net_Adapter__NDIS_Driver__and_General_Commands"></span><span id="net_adapter__ndis_driver__and_general_commands"></span><span id="NET_ADAPTER__NDIS_DRIVER__AND_GENERAL_COMMANDS"></span>ネット アダプター、NDIS ドライバー、および一般的なコマンド


次のコマンドは、マシンのネットワーク アダプター、ネットワーク ドライバー、および一般的なコマンドを (rcvqueues が開き、フィルター、Oid、および RW ロック) と、ネットワーク スタックに関連付けられているに関する情報を表示します。

-   [ **!ndiskd.netadapter**](-ndiskd-netadapter.md)
-   [ **!ndiskd.minidriver**](-ndiskd-minidriver.md)
-   [ **!ndiskd.rcvqueue**](-ndiskd-rcvqueue.md)
-   [ **!ndiskd.protocol**](-ndiskd-protocol.md)
-   [ **!ndiskd.mopen**](-ndiskd-mopen.md)
-   [ **!ndiskd.filter**](-ndiskd-filter.md)
-   [ **!ndiskd.filterdriver**](-ndiskd-filterdriver.md)
-   [ **!ndiskd.oid**](-ndiskd-oid.md)
-   [ **!ndiskd.ndisrwlock**](-ndiskd-ndisrwlock.md)
-   [ **!ndiskd.netreport**](-ndiskd-netreport.md)

## <a name="span-idnetbufferlistandnetbuffercommandsspanspan-idnetbufferlistandnetbuffercommandsspanspan-idnetbufferlistandnetbuffercommandsspannetbufferlist-and-netbuffer-commands"></a><span id="NET_BUFFER_LIST_and_NET_BUFFER_Commands"></span><span id="net_buffer_list_and_net_buffer_commands"></span><span id="NET_BUFFER_LIST_AND_NET_BUFFER_COMMANDS"></span>NET\_バッファー\_一覧と NET\_バッファー コマンド


次のコマンドに関連する情報を表示する[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)と[ **NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)構造体。

-   [ **!ndiskd.nbl**](-ndiskd-nbl.md)
-   [ **!ndiskd.nb**](-ndiskd-nb.md)
-   [ **!ndiskd.nblpool**](-ndiskd-nblpool.md)
-   [ **!ndiskd.nbpool**](-ndiskd-nbpool.md)
-   [ **!ndiskd.pendingnbls**](-ndiskd-pendingnbls.md)
-   [ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

## <a name="span-idnetadaptercxcommandsspanspan-idnetadaptercxcommandsspanspan-idnetadaptercxcommandsspannetadaptercx-commands"></a><span id="NetAdapterCx_Commands"></span><span id="netadaptercx_commands"></span><span id="NETADAPTERCX_COMMANDS"></span>NetAdapterCx コマンド


次のコマンドは、ネットワーク アダプター WDF クラス拡張機能 (NetAdapterCx) に関連する情報を表示\[LINK TBD\]および関連付けられている構造体、NET\_リング\_バッファー \[LINK TBD\] net\_パケット\[LINK TBD\]します。

-   [ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)
-   [ **!ndiskd.netqueue**](-ndiskd-netqueue.md)
-   [ **!ndiskd.netrb**](-ndiskd-netrb.md)
-   [ **!ndiskd.netpacket**](-ndiskd-netpacket.md)
-   [ **!ndiskd.netpacketfragment**](-ndiskd-netpacketfragment.md)

## <a name="span-idnetworkinterfacecommandsspanspan-idnetworkinterfacecommandsspanspan-idnetworkinterfacecommandsspannetwork-interface-commands"></a><span id="Network_Interface_Commands"></span><span id="network_interface_commands"></span><span id="NETWORK_INTERFACE_COMMANDS"></span>ネットワーク インターフェイスのコマンド


次のコマンドは、ネットワーク インターフェイスに関連する情報を表示します。

-   [ **!ndiskd.interfaces**](-ndiskd-interfaces.md)
-   [ **!ndiskd.ifprovider**](-ndiskd-ifprovider.md)

## <a name="span-idndispacketcommandsspanspan-idndispacketcommandsspanspan-idndispacketcommandsspanndispacket-commands"></a><span id="NDIS_PACKET_Commands"></span><span id="ndis_packet_commands"></span><span id="NDIS_PACKET_COMMANDS"></span>NDIS\_パケット コマンド


次のコマンドに関する情報を表示する[NDIS\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造体。 これらの拡張機能では、従来の NDIS 5.x ドライバーです。 NDIS\_パケットの構造とその関連付けられているアーキテクチャが使用されなくなりました。

-   [ **!ndiskd.pkt**](-ndiskd-pkt.md)
-   [ **!ndiskd.pktpools**](-ndiskd-pktpools.md)
-   [ **!ndiskd.findpacket**](-ndiskd-findpacket.md)

## <a name="span-idcondiscommandsspanspan-idcondiscommandsspanspan-idcondiscommandsspancondis-commands"></a><span id="CoNDIS_Commands"></span><span id="condis_commands"></span><span id="CONDIS_COMMANDS"></span>いる CoNDIS コマンド


次のコマンドに関する情報を表示する[Connection-Oriented NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)接続します。

-   [ **!ndiskd.vc**](-ndiskd-vc.md)
-   [ **!ndiskd.af**](-ndiskd-af.md)

## <a name="span-idndisdebuggingcommandsspanspan-idndisdebuggingcommandsspanspan-idndisdebuggingcommandsspanndis-debugging-commands"></a><span id="NDIS_Debugging_Commands"></span><span id="ndis_debugging_commands"></span><span id="NDIS_DEBUGGING_COMMANDS"></span>NDIS デバッグ コマンド


次のコマンドは、NDIS refcounts、イベント ログ、スタック トレース、およびデバッグ トレースに関連する情報を表示します。

-   [ **!ndiskd.ndisref**](-ndiskd-ndisref.md)
-   [ **!ndiskd.ndisevent**](-ndiskd-ndisevent.md)
-   [ **!ndiskd.ndisstack**](-ndiskd-ndisstack.md)
-   [ **!ndiskd.dbglevel**](-ndiskd-dbglevel.md)
-   [ **!ndiskd.dbgsystems**](-ndiskd-dbgsystems.md)

## <a name="span-idwdicommandsspanspan-idwdicommandsspanspan-idwdicommandsspanwdi-commands"></a><span id="WDI_Commands"></span><span id="wdi_commands"></span><span id="WDI_COMMANDS"></span>WDI コマンド


次のコマンドに関する情報を表示する[WDI ミニポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)します。

-   [ **!ndiskd.wdiadapter**](-ndiskd-wdiadapter.md)
-   [ **!ndiskd.wdiminidriver**](-ndiskd-wdiminidriver.md)
-   [ **!ndiskd.nwadapter**](-ndiskd-nwadapter.md)

## <a name="span-idndisandndiskdinformationcommandsspanspan-idndisandndiskdinformationcommandsspanspan-idndisandndiskdinformationcommandsspanndis-and-ndiskd-information-commands"></a><span id="NDIS_and__ndiskd_Information_Commands"></span><span id="ndis_and__ndiskd_information_commands"></span><span id="NDIS_AND__NDISKD_INFORMATION_COMMANDS"></span>NDIS および! ndiskd 情報コマンド


次のコマンドは、NDIS.sys と ndiskd.dll に関する情報を表示します。

-   [ **!ndiskd.ndis**](-ndiskd-ndis.md)
-   [ **!ndiskd.ndiskdversion**](-ndiskd-ndiskdversion.md)

## <a name="span-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanmiscellaneous-commands"></a><span id="Miscellaneous_Commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>その他のコマンド


-   [ **! ndiskd.ifstacktable**](-ndiskd-ifstacktable.md)
-   [ **!ndiskd.compartments**](-ndiskd-compartments.md)
-   [ **!ndiskd.ndisslot**](-ndiskd-ndisslot.md)

## <a name="span-idrelatedtopicsspanspan-idrelatedtopicsspanspan-idrelatedtopicsspanrelated-topics"></a><span id="Related_Topics"></span><span id="related_topics"></span><span id="RELATED_TOPICS"></span>関連トピック


参照の Windows Vista 以降、ドライバー NDIS の設計の詳細については、[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)します。

Windows Vista 以降の NDIS ドライバーへの参照の詳細については、次を参照してください。 [Windows Vista との参照を後でネットワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

使用しての例については、!、ネットワーク スタックをデバッグする ndiskd デバッガー コマンドを参照してください[ネットワーク スタックをデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)します。

 

 






