---
title: NDIS 仮想マシン (VM) 共有メモリのセキュリティ上の問題
description: NDIS 仮想マシン (VM) 共有メモリのセキュリティ上の問題
ms.assetid: 42b903b0-6729-4314-9305-9345fff9b2ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c574d7cd2f299ae12234ff62ba5da27dcf406d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382125"
---
# <a name="security-issues-with-ndis-virtual-machine-vm-shared-memory"></a>NDIS 仮想マシン (VM) 共有メモリのセキュリティ上の問題





このトピックでは、仮想マシン キュー (VMQ) の受信バッファーの仮想マシン (VM) から共有メモリの割り当てに関連する潜在的なセキュリティの問題について説明します。 トピックには、次のセクションが含まれています。

-   [共有メモリを VM のセキュリティの問題の概要](#overview)

-   [Windows Server 2008 R2 セキュリティの問題に対処する方法](#ndis620)

-   [Windows Server 2012 およびそれ以降のバージョンのセキュリティの問題を解決する方法](#ndis630)

**注**  で、HYPER-V 子パーティションは、VM でとも呼ばれます。

 

### <a href="" id="overview"></a>共有メモリを VM のセキュリティの問題の概要

Vm は、信頼されているソフトウェア エンティティではありません。 つまり、悪意のある VM を他の Vm または HYPER-V 親パーティションで実行されている管理オペレーティング システムに干渉することできません必要があります。 このセクションでは、背景情報とドライバー開発者が VMQ セキュリティの問題と共有メモリの要件を理解していることを確認するための要件を示します。 共有メモリの詳細については、次を参照してください。、[共有メモリ リソース割り当て](shared-memory-resource-allocation.md)でトピック、[書き込み VMQ ドライバー](writing-vmq-drivers.md)セクション。

仮想化された環境では、VM が共有メモリを表示したり、VM で変更することができます。 ただし、表示、または他の Vm に関連付けられているデータの変更は許可されません。 Vm はもアドレス空間の運用管理にアクセスする許可されません。

受信したパケットのヘッダー部分を保護する必要があります。 VM は、ネットワークの仮想サービス プロバイダー (VSP) での HYPER-V 拡張可能スイッチの動作に影響を与えるには許可されません。 そのため、VLAN (仮想 LAN) のフィルター処理する必要があります発生ネットワーク アダプターでは、DMA は転送する前に VM にデータがメモリを共有します。 また、スイッチのメディア アクセス制御 (MAC) アドレスの学習は影響ことはできません。

HYPER-V 拡張可能スイッチの場合は、VM に接続されているポートが関連付けられている VLAN 識別子、ホスト コンピューターでは、宛先の MAC アドレスと受信のフレームの VLAN 識別子にホストする前に、ポートの各属性が一致するを確認する必要があります。VM の仮想ネットワーク アダプターにパケットを転送します。 フレームの VLAN 識別子で、ポートの VLAN id が一致しない場合、パケットは破棄されます。 ホストのメモリから仮想ネットワーク アダプターの受信バッファーが割り当てられると、ホストは VLAN 識別子を確認し、ターゲット VM に表示されるフレームのコンテンツを行う前に必要な場合、フレームをドロップできます。 フレームは、VM のアドレス空間にはコピーされず場合、は、その VM からアクセスできません。

ただし、VMQ は共有メモリを使用するのにように構成、ネットワーク アダプターは、VM のアドレス空間に直接受信フレームを転送するのに DMA を使用します。 この転送では、VM が必要な VLAN のフィルターを適用する拡張可能スイッチを待つことがなく、受信したフレームの内容を調べることができます、セキュリティ上の問題について説明します。

### <a href="" id="ndis620"></a>Windows Server 2008 R2 セキュリティの問題に対処する方法

Windows Server 2008 r2、VSP が、VM のアドレス空間から割り当てられている共有メモリを使用する VM のキューを構成する前に次のテストのフィルター処理を使用、キューのします。

```syntax
(MAC address == x) && (VLAN identifier == n)
```

ネットワーク アダプターのハードウェアでは、受信バッファーへの DMA 転送する前に、このテストでサポートできる場合、ネットワーク アダプターする無効な VLAN 識別子を持つフレームの脱落か拡張可能スイッチで除外することができるように、既定のキューに送信します。 ミニポート ドライバーは、このテストを使用したキューにフィルターを設定する要求に成功すると、拡張可能スイッチは、そのキューの共有 VM メモリを使用できます。 ただし、ネットワーク アダプターのハードウェアが接続先 MAC アドレスと VLAN 識別子の両方に基づいてフレームをフィルター処理できない場合、拡張可能スイッチは、そのキューの共有ホストのメモリを使用します。

拡張可能スイッチは送信フレームのルーティング情報を構成する受信のフレームの MAC アドレスのソースを検査、つまり learning 物理スイッチに似ています。 ホストはスタックでファイアウォール フィルター ドライバーをインストールすることはたとえば、上と下、拡張可能なネットワーク アダプターのハードウェアのミニポート ドライバーには、ドライバーを切り替えます。 ファイアウォール フィルター ドライバーは、拡張可能スイッチの前に受信したフレーム内のデータにアクセスできます。 VM のアドレス空間から各フレームの受信バッファー全体が割り当てられると、悪意のある VM はフィルター ドライバーまたはホストで実行されている拡張可能スイッチのいずれかが検査はフレームの部分にアクセスでした。

VM を使用して VM のキューのメモリを共有するときに、このセキュリティ問題に対処するネットワーク アダプターは先読みサイズは、これは、事前に定義された固定値では、少なくともバイト オフセット位置にパケットを分割する必要があります。 先読みデータ-先読みサイズのバイト オフセットは、意味データ-先読みデータに割り当てられていた共有メモリに DMA を転送する必要があります。 Post 先読みデータ: フレームのペイロードの残りの部分、DMA post 先読みデータに割り当てられていた共有メモリに転送する必要があります。

次の図は、ネットワークの関係のデータ構造を示しています先読みアサーションと後先読みに受信したデータを分割するときにメモリ バッファーを共有します。

![先読みアサーションと後先読みのデータを含む vmq パケットの構造体を示す図](images/vmqpacket.png)

VMQ が共有メモリの概要の要件は次のとおりです。

-   ネットワーク アダプターを先読みのサイズを超えるネットワーク ヘッダー境界で受信したフレームに分割できます。 ただし、NDIS、および例外なく要求されると、すべてのフレームが受信され、VMQ に割り当てられている必要があります分割以降 NDIS 要求先読みサイズの境界にあります。

-   先読みデータは、ミニポート ドライバーによって割り当てられている共有メモリに DMA を転送する必要があります。 ミニポート ドライバーは、先読みのデータのメモリが使用されること、割り当ての呼び出しで指定する必要があります。

-   Post 先読みデータは、ミニポート ドライバーによって割り当てられている共有メモリに DMA を転送する必要があります。 ミニポート ドライバーは、post 先読みデータのメモリが使用されること、割り当ての呼び出しで指定する必要があります。

-   ミニポート ドライバーをどのアドレス空間の NDIS を使用して、共有メモリの割り当て要求の完了に依存することはできません。 つまり、先読みまたは post 先読みのデータの共有メモリ アドレス空間は、特定の実装です。 多くの場合、NDIS または拡張可能スイッチは、ホストのメモリ アドレス空間からの投稿先読み使用するためのものも含め、すべての要求を満たす可能性があります。

-   フレームに、VMQ が受信される順序が表示されるそのキュー内のフレームがドライバー スタックを示されたときに、キューを保持する必要があります。

-   ネットワーク アダプターには、各 post lookahead バッファーに十分なバックフィル メモリ領域を割り当てる必要があります。 この割り当ては、先読みのデータをバックフィル部分、post lookahead バッファーにコピーする許可し、連続したバッファー内の VM への配信にフレームを使用します。

VMQ のこれらの要件を満たすハードウェアでメカニズム共有メモリがない場合は、受信側では、スキャッター/ギャザー DMA をサポートするハードウェアは、受信した各フレームの 2 つの受信バッファーを割り当てることによって、同じ結果を得る可能性があります。 この場合、最初のバッファーのサイズは先読みアサーションが要求されたサイズに制限されています。

VMQ のこれらの要件が任意のメソッドによってメモリを共有ネットワーク アダプターが満たすことができない場合は、VSP にメモリを割り当てる、VMQ がホストのアドレス空間からの受信バッファーとは、コピー、受信したネットワーク アダプターからのパケットは VM アドレスへのバッファーを受信領域。

### <a href="" id="ndis630"></a>Windows Server 2012 およびそれ以降のバージョンのセキュリティの問題を解決する方法

Windows Server 2012 以降、VSP は割り当てられません共有メモリ、VM から、VMQ 受信バッファー。 代わりに、ホストのアドレス空間からの受信バッファーを VMQ とコピー、ネットワーク アダプターから受信したパケットが VM のアドレス空間をバッファーを受信し、VSP はメモリを割り当てます。

次の点は、Windows Server 2012、Windows の以降のバージョンで実行される VMQ ミニポート ドライバーに適用されます。

-   6\.20 VMQ の NDIS ミニポート ドライバーでは、変更は必要ありません。 ただし、場合、VSP VM キューには、割り当ての OID (オブジェクト識別子) メソッドの要求を発行[OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)、設定、 **LookaheadSize**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体をゼロにします。 これより前の先読みアサーションと post lookahead バッファーにパケットを分割されずに、ミニポート ドライバー。

-   NDIS 6.30 以降、VMQ ミニポート ドライバーはする必要がありますより前の先読みアサーションと post lookahead バッファーにパケット データを分割のサポートをアドバタイズしません。 初期化するときは、これらの規則を従う必要があります、ミニポート ドライバーがその VMQ 機能を登録する場合、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

    -   ミニポート ドライバーを設定する必要がありますいない、 **NDIS\_受信\_フィルター\_先読み\_分割\_サポートされている**フラグ、**フラグ**メンバー。

    -   ミニポート ドライバーを設定する必要があります、 **MinLookaheadSplitSize**と**MinLookaheadSplitSize**メンバーをゼロにします。

    VMQ 機能を登録する方法の詳細については、次を参照してください。[ネットワーク アダプターの VMQ 機能を判断する](determining-the-vmq-capabilities-of-a-network-adapter.md)します。

 

 





