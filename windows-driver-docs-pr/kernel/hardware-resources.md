---
title: ハードウェア リソース
description: ハードウェア リソース
ms.assetid: c7a6997b-34f9-4dd9-b384-2321a8b5ce54
keywords:
- リソース記述子の WDK PnP
- PnP WDK カーネル、ハードウェアリソース
- WDK カーネル、ハードウェアリソースのプラグアンドプレイ
- リソース要件 WDK PnP の一覧表示
- リソース一覧 WDK PnP
- 割り当てられたリソース WDK PnP
- 要件 WDK PnP の一覧
- レジストリ WDK PnP
- 論理構成 WDK PnP
- ブート構成 WDK PnP
- 強制構成 WDK PnP
- フィルター処理された構成 (WDK PnP)
- 構成の上書き WDK PnP
- 構成の種類 WDK PnP
- 割り当てられた構成 (WDK PnP)
- 基本的な構成 (WDK PnP)
- ハードウェア リソース
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e22ef29044d442186f668ed1dfc88ec4a7cf6a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838645"
---
# <a name="hardware-resources"></a>ハードウェア リソース





ハードウェアリソースは、周辺機器とシステムプロセッサが相互に通信できるようにする、割り当て可能で、アドレス指定可能なバスパスです。 通常、ハードウェアリソースには、i/o ポートアドレス、割り込みベクター、およびバス相対メモリアドレスのブロックが含まれます。

システムが*デバイスインスタンス*と通信する前に、PnP マネージャーは、使用可能なリソースとデバイスインスタンスが使用できるリソースに関する情報に基づいて、デバイスインスタンスにハードウェアリソースを割り当てる必要があります。 リソースは、デバイス[ツリー](device-tree.md)内の各デバイスノードに割り当てられます (表示されているデバイスにリソースが必要で、それらのリソースが使用可能であることを前提としています)。 PnP マネージャーは、デバイスノードに関連付けられているリストを使用して、ハードウェアリソースを追跡します。 次の2種類のリストを使用します。

<a href="" id="resource-requirements-list"></a>*リソース要件の一覧*  
デバイスは、通常、リソース割り当ての範囲内で動作するように設計されています。 たとえば、デバイスに必要な割り込みベクターは1つだけですが、ベクターの範囲のいずれかを使用できる場合があります。 デバイスインスタンスごとに、PnP マネージャーは、デバイスが動作できるハードウェアリソースの範囲をすべて指定する*リソース要件の一覧*を保持します。 リストの名前は、デバイスに割り当てるときに、PnP マネージャーがこの一覧からリソースを選択する必要があるという事実から由来します。

カーネルモードコードでは、 [**IO\_リソース\_要件\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)構造 (システムルーチンへの入力または irp への応答) を使用したリソース要件の一覧を指定します。 ユーザーモードのコードでは、pnp 構成マネージャーの[構造](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))を使用して[pnp 構成マネージャー関数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))への入力として、リソース要件リストを指定します。

<a href="" id="resource-list"></a>*リソースの一覧*  
PnP マネージャーは、デバイスにリソースを割り当てるときに、各デバイスインスタンスに割り当てられたリソースの一覧を作成することによって、これらの割り当てを追跡します。 これらのリストは*リソース割り当てリスト*と呼ばれる場合がありますが、その名前は通常、*リソースリスト*にショートされます。 PnP マネージャーは、デバイスがシステムに追加されるかシステムから削除されたときに、リソースの一覧の内容を変更することができ、その後、リソースが再割り当てされます。 (リソースは、PnP BIOS でも割り当てることができます。 また、INF ファイルまたはユーザー入力を使用してインストールソフトウェアを実行すると、特定のリソースをデバイスに割り当てることができます。

カーネルモードコードでは、 [**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)構造体 (システムルーチンへの入力または irp への応答として) を使用して、リソースリストを指定します。 ユーザーモードのコードでは、pnp 構成マネージャーの[構造](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))を使用して[pnp 構成マネージャーの関数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))への入力として、リソースリストを指定します。

PnP マネージャーは、リソース要件リストとリソースリストをレジストリに格納します。このリストは、Regedit.exe を使用して表示できます。 ドライバーは、[プラグアンドプレイルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)と[プラグアンドプレイの小さな irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)を通じて、これらの一覧に間接的にアクセスできます。 ユーザーモードアプリケーションでは、 [PnP 構成マネージャーの関数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))を使用できます。 (ドライバーとアプリケーションは、将来のリリースで変更される可能性があるため、レジストリ機能を使用してこれらの一覧に直接アクセスすることはできません)。

### <a href="" id="ddk-logical-configurations-kg"></a>論理構成

リソース要件リストとリソースリストの両方に1つ以上の*論理構成*が含まれています。 各論理構成は、許容されるリソースの範囲、または特定の*デバイスインスタンス*の特定のリソースのセットを識別します。 さらに、デバイスインスタンスの各論理構成は、*論理構成の種類*のいずれかに属します。 構成の種類は次のとおりです。 同じ種類または異なる種類の複数の論理構成が、各デバイスインスタンスに割り当てられる場合があります。

### <a name="logical-configuration-types-for-resource-requirements-lists"></a>リソース要件の一覧の論理構成の種類

<a href="" id="basic-configuration"></a>*基本構成*  
リソース要件一覧は、プラグアンドプレイデバイスによって提供されるリソース範囲を識別します。 ドライバーは、 [**irp\_\_クエリ\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)の irp を受信すると、この一覧を返します。 (PnP 以外のデバイスの基本的な構成については、「INF ファイル」を参照してください。 この場合、デバイスのインストールソフトウェアは INF ファイルを読み取り、 [PnP 構成マネージャーの関数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))を呼び出して要件リストを作成します。

<a href="" id="filtered-configuration"></a>*フィルター処理された構成*  
[**Irp\_\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)の irp に応答して、ドライバースタックに渡され、ドライバースタックによって返されたリソース要件の一覧。 PnP マネージャーは、結果として得られるフィルター処理された構成をリソース割り当ての基礎として使用します。

<a href="" id="override-configuration"></a>*構成の上書き*  
基本構成を上書きするリソース要件の一覧。 通常、デバイスインストーラーでは、デバイスの INF ファイルに[**Inf DDInstall. LogConfigOverride セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)が含まれている場合、上書き構成が作成されます。 上書き構成は、そのデバイスがシステムから物理的に削除されても削除されません。

### <a name="logical-configuration-types-for-resource-lists"></a>リソースリストの論理構成の種類

<a href="" id="boot-configuration"></a>*ブート構成*  
システムが起動されたときにデバイスインスタンスに割り当てられたリソースを識別するリソースリスト。 (PnP デバイスの場合は、BIOS によって提供される構成です。 PnP 以外のデバイスの場合、これらのリソースはカードのジャンパーによって選択される可能性があります)。ドライバーは、Irp を受信したときにこのリソースリストを返し、 [ **\_クエリ\_リソース**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)の irp を\_します。 (デバイスで使用されているすべてのリソースを BIOS が特定できない場合は、ブート構成が一部空になることがあります)。デバイスが削除または再起動された場合、PnP マネージャーはこの一覧を変更できます。 非 PnP デバイスの場合は、この構成の種類を強制構成の代わりに使用できます。この場合、構成の優先順位は同等の強制構成よりも低くなります。 デバイスインスタンスごとに1つのブート構成しか存在できません。

<a href="" id="forced-configuration"></a>*強制構成*  
デバイスインスタンスで使用する必要があるリソースを識別するリソースリスト。 強制構成を行うと、PnP マネージャーはデバイスインスタンスに他のリソースを割り当てることができなくなります。 デバイスのインストーラーでは、INF に含まれている情報またはユーザーから受信した情報に基づいて、強制構成が作成される場合があります。 強制構成は、デバイスがシステムから物理的に削除されても削除されません。 デバイスインスタンスごとに1つの強制構成しか存在できません。

<a href="" id="allocated-configuration"></a>*割り当てられた構成*  
デバイスインスタンスによって現在使用されているリソースを識別するリソースリスト。 割り当てられた構成は、デバイスインスタンスごとに1つだけ存在できます。

デバイスドライバーは、PnP 互換デバイスの基本構成、フィルター処理された構成、およびブート構成を決定し、PnP マネージャーによって送信される Irp に応答してその情報を返す役割を担います。 (詳細については、「[実行中のシステムへの PnP デバイスの追加](adding-a-pnp-device-to-a-running-system.md)」を参照してください)。ドライバーのインストールソフトウェアでは、上書き構成、強制構成、および非 PnP デバイスのブート構成を作成できます。 PnP マネージャーは、各デバイスインスタンスに割り当てられた構成を保持します。

各構成が作成されるときに、優先度が割り当てられます。 デバイスインスタンスに同じ種類の複数の論理構成が割り当てられていることが PnP マネージャーによって検出された場合は、優先順位が最も高いものを最初に使用しようとします。 その構成によってリソースの競合が発生した場合は、次に低い優先順位で構成が試行されます。 (構成の優先順位の一覧については、「 [**CM\_Add\_Empty\_Log\_Conf**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_add_empty_log_conf)」を参照してください)。

 

 




