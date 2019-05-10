---
title: 受信フィルター機能の判断
description: 受信フィルター機能の判断
ms.assetid: 11EE5987-A2DE-4388-86D0-77285453E80A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cc3ec7bbea2f7695ac98ceacb5b795d45066b21
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405147"
---
# <a name="determining-receive-filtering-capabilities"></a>受信フィルター機能の判断


このトピックでは、NDIS と関連付けたドライバーがシングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの受信のフィルター処理機能を特定する方法について説明します。 このトピックの内容は次のとおりです。

[中にフィルター処理機能を受け取る reporting *MiniportInitializeEx*](#reporting-receive-filtering-capabilities-during-miniportinitializeex)

[ドライバーに関連してフィルター処理機能を受信するクエリを実行します。](#querying-receive-filtering-capabilities-by-overlying-drivers)

**注**  ミニポート ドライバー、PCI Express (PCIe) 物理機能 (PF) の SR-IOV ネットワーク アダプターを報告できるため受信フィルタ リング機能のみです。 PCIe 仮想機能 (Vf) 用のミニポート ドライバーでは、SR-IOV 対応のアダプターの機能をフィルター処理、受信を報告する必要があります。

 

## <a name="reporting-receive-filtering-capabilities-during-miniportinitializeex"></a>中にフィルター処理機能を受け取る reporting *MiniportInitializeEx*


NDIS が PF ミニポート ドライバーを呼び出すときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーには、次のフィルター機能が表示されます。

-   完全なハードウェアでは、フィルター処理機能をサポートできるネットワーク アダプターが表示されます。

-   受信側のネットワーク アダプターで現在有効になっているインターフェイスのフィルタ リング機能。

完全なハードウェア受信フィルター処理機能を基になるネットワーク アダプターのミニポート ドライバー レポート、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)次のように初期化された構造体。

1.  ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

    NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_フィルター\_機能\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_受信\_フィルター\_機能\_リビジョン\_2。

2.  ミニポート ドライバーの設定の他のメンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)受信フィルターの値の範囲に構造体SR-IOV ネットワーク アダプターの機能。 ミニポート ドライバーが適切なフラグを設定するなど、 **SupportedFilterTests**ミニポート ドライバーがサポートするフィルターのテスト操作を指定します。

3.  受信、SR-IOV だけでなく、次のインターフェイスにも使用のフィルター処理します。

    -   [NDIS パケット結合](ndis-packet-coalescing.md)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](managing-packet-coalescing-receive-filters.md)します。

    -   [バーチャル マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](setting-and-clearing-vmq-filters.md)します。

    メンバーが設定する必要がありますもミニポート ドライバーでは、これらのインターフェイスのいずれかをサポートする場合、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体を範囲には、インターフェイスに固有のフィルター処理の機能の値が表示されます。 たとえば、ドライバーは、NDIS パケットを結合し、SR-IOV をサポートする場合は、設定があります、NDIS\_受信\_フィルター\_パケット\_COALESCING\_サポートされている\_ON\_既定の\_キュー フラグ、 **SupportedQueueProperties**メンバー。

ミニポート ドライバー レポートを通じて基になるネットワーク アダプターのフィルター機能が表示される現在が有効な[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)次のように初期化された構造体。

1.  ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

    NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_フィルター\_機能\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_受信\_フィルター\_機能\_リビジョン\_2。

2.  ミニポート ドライバーの設定の他のメンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)受信フィルターの値の範囲に構造体現在有効になっている、インターフェイスの機能です。 たとえば、NDIS パケットの結合が有効になっている場合、ドライバーする必要がありますこのテクノロジに固有のメンバーを設定のみです。

    インターフェイスを使用するがフィルター処理に受信は有効になっているか、標準化された INF キーワードによって無効になっています。 NDIS パケットの結合が有効にする方法の詳細については、次を参照してください。[パケットの結合の標準化された INF キーワード](standardized-inf-keywords-for-packet-coalescing.md)します。 SR-IOV と VMQ が有効にする方法の詳細については、次を参照してください。[処理、SR-IOV、VMQ、および RSS の標準化された INF キーワード](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)します。

NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーは、次の手順に従って、ネットワーク アダプターの機能をフィルター処理、受信を登録します。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

    ミニポート ドライバーのセット、 **HardwareReceiveFilterCapabilities**メンバーのアドレスを[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。 この構造体が、完全なで先ほど初期化ハードウェアは、ネットワーク アダプターのフィルター機能を受信します。

2.  VMQ、SR-IOV、および NDIS パケット結合は、ネットワーク アダプターの中のすべて無効にした場合、ミニポート ドライバーの設定、 **CurrentReceiveFilterCapabilities**メンバーを NULL にします。

3.  VMQ、SR-IOV、または NDIS パケットの結合が、ネットワーク アダプターで現在有効で、ミニポート ドライバーが、次の操作にする必要があります。

    -   ミニポート ドライバーを初期化する必要があります別[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体を現在のフィルター処理機能を受信します。ネットワーク アダプターで現在有効になっているインターフェイスです。

        SR-IOV インターフェイスが有効になっている場合は、状況、ミニポート ドライバーがのメンバーを設定する必要があります、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)を同じまたは別の値構造体。 これは、SR-IOV インターフェイスと同様のキュー メカニズムを提供します、VMQ を使用して仮想ポート (拡張) VM ではなく受信キューのためです。

        たとえば、ミニポート ドライバーは、NDIS を設定する必要があります\_受信\_フィルター\_VMQ\_フィルター\_有効フラグ、 **EnabledFilterTypes**場合は、いずれかのメンバー、VMQ またはSR-IOV のインターフェイスを有効にします。 ただし、ミニポート ドライバーを設定する必要があります、 **NumQueues**メンバー SR-IOV インターフェイスが有効になっている場合は 0 および VMQ インターフェイスが有効になっている場合は 0 以外の値。

    -   ミニポート ドライバーのセット、 **CurrentReceiveFilterCapabilities**メンバーのアドレスを[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)現在を含む構造体が現在有効になっているインターフェイスのフィルター処理機能を受信します。

4.  VMQ、SR-IOV、または NDIS パケットの結合が、ネットワーク アダプターで現在有効で、ミニポート ドライバー設定、 **HardwareReceiveFilterCapabilities**メンバーのアドレスを[ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。 この構造体がで先ほど初期化現在が有効なネットワーク アダプターのフィルター処理機能を受信します。

5.  ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

## <a name="querying-receive-filtering-capabilities-by-overlying-drivers"></a>ドライバーに関連してフィルター処理機能を受信するクエリを実行します。


ネットワーク アダプターの現在の有効な NDIS パスには、関連の次のようにネットワーク アダプターにバインドするドライバーをフィルター処理機能が表示されます。

-   NDIS が上にあるフィルター ドライバーを呼び出すときに[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)関数、NDIS 渡しますネットワーク アダプターの NIC のスイッチ機能を通じて、 *AttachParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。 **ReceiveFilterCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

-   NDIS が上位のプロトコル ドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数、NDIS 渡しますネットワーク アダプターの NIC のスイッチ機能を通じて、 *BindParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。 **ReceiveFilterCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

NDIS も返されます、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864) のオブジェクト識別子(OID)のクエリ要求を処理する場合に構造体[OID\_受信\_フィルター\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569786)と[OID\_受信\_フィルター\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569791)関連プロトコルまたはフィルター ドライバーによって発行されます。

 

 





