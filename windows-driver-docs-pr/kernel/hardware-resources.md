---
title: ハードウェア リソース
description: ハードウェア リソース
ms.assetid: c7a6997b-34f9-4dd9-b384-2321a8b5ce54
keywords:
- リソースの記述子 PnP WDK
- PnP WDK カーネルでは、ハードウェア リソース
- プラグ アンド プレイ WDK カーネルでは、ハードウェア リソース
- PnP WDK リソース要件の一覧
- リソースには、WDK PnP が一覧表示されます。
- 割り当てられた PnP WDK リソース
- 要件には、WDK PnP が一覧表示されます。
- レジストリ PnP WDK
- PnP WDK の論理構成
- ブート構成 PnP WDK
- 強制構成 PnP WDK
- フィルター選択された構成 PnP WDK
- PnP WDK の構成を上書き
- PnP WDK の構成の種類
- PnP WDK の構成の割り当てください。
- PnP WDK の基本構成
- ハードウェア リソース
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0872ce250ca7e0a48f4fa226452eb2a2942a712
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371882"
---
# <a name="hardware-resources"></a>ハードウェア リソース





ハードウェア リソースは、周辺機器とシステムのプロセッサを互いに通信を許可するバスの割り当て可能なアドレス指定可能なパスです。 通常、ハードウェア リソースには I/O ポートのアドレスには、ベクトル割り込みにはのバスの相対メモリ アドレスのブロックが含まれます。

システムと通信できる前に、*デバイス インスタンス*、PnP マネージャーは、どのリソースが使用可能とするデバイスのインスタンスを使用できるは、サポート技術情報に基づくデバイス インスタンスにハードウェア リソースを割り当てる必要があります. リソースは、各デバイス ノードに割り当てられている、[デバイス ツリー](device-tree.md) (仮定表されるデバイス リソースを必要として、それらのリソースを利用)。 PnP マネージャーは、ハードウェア リソースのリストで、デバイスのノードに関連付けるを使用するを追跡します。 2 つの種類のリストを使用します。

<a href="" id="resource-requirements-list"></a>*リソース要件の一覧*  
デバイスは通常、リソースの割り当ての範囲内で動作するに設計されています。 たとえばをデバイスには、1 つだけの割り込みベクトルが必要とする可能性がありますが、ベクターの範囲のいずれかを使用できる場合があります。 デバイス インスタンスごとに、PnP マネージャーは、*リソース要件の一覧*すべてのデバイスの操作に使用できるハードウェア リソースの範囲を指定します。 PnP マネージャーがデバイスに割り当てるときに、この一覧からリソースを選択する必要があるという事実から、リストの名前が付けられています。

カーネル モード コードを使用してリソース要件の一覧を指定する[ **IO\_リソース\_要件\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_resource_requirements_list) (システムのルーチンへの入力としていずれかの構造体または、Irp への応答)。 ユーザー モード コードを使用してリソース要件の一覧を指定する[configuration manager の構造体の PnP](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))への入力として[構成マネージャーの機能の PnP](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))します。

<a href="" id="resource-list"></a>*リソースの一覧*  
PnP マネージャーでは、デバイスにリソースを割り当てるを追跡これらの割り当てをデバイス インスタンスごとに割り当てられたリソースの一覧を作成します。 これらのリストを呼び出すことができます*リソースの割り当て一覧*が、その名前は通常にショート*リソースの一覧*します。 リソースが再割り当て、その後、デバイスの追加またはシステムから削除、PnP マネージャーでリソース一覧の内容を変更できます。 (リソースも割り当てることができますを加えました。 インストール ソフトウェアも、: INF ファイル、またはユーザーの入力を使用して、デバイスに特定のリソースを割り当てる PnP マネージャーを強制できます)。

カーネル モード コードを使用してリソースの一覧を指定する[ **CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list) (か、入力システム ルーチンまたは Irp への応答として) 構造体。 ユーザー モード コードを使用してリソースの一覧を指定する[configuration manager の構造体の PnP](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))への入力として[構成マネージャーの機能の PnP](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))します。

PnP マネージャーには、Regedit.exe を使用して表示できます、レジストリ内のリソース要件の一覧とリソースの一覧が格納されます。 ドライバーを通じて間接的にこれらのリストにアクセスできる[プラグ アンド プレイ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[プラグ アンド プレイ マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)します。 ユーザー モード アプリケーションで使用できます[構成マネージャーの機能の PnP](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))します。 (ドライバーとアプリケーションする必要がありますいない直接アクセス ストレージ形式は、将来のリリースで変更されるため、レジストリの関数を使用してこれらのリスト)。

### <a href="" id="ddk-logical-configurations-kg"></a>論理構成

リソース要件の一覧とリソースの一覧の両方が 1 つまたは複数を含む*論理構成*します。 各論理構成が、許容可能なリソースの範囲または特定の特定のリソースのセットのいずれかを識別する*デバイス インスタンス*します。 デバイス インスタンスに対する各構成の論理がさらのいずれかに属している、*論理構成の種類*します。 構成の種類は、以下に示します。 同じまたは別の種類の複数の論理構成は、各デバイス インスタンスに割り当てられる可能性があります。

### <a name="logical-configuration-types-for-resource-requirements-lists"></a>リソース要件の一覧の論理構成の種類

<a href="" id="basic-configuration"></a>*基本的な構成*  
リソース要件は、プラグ アンド プレイ デバイスによって提供される特定のリソース範囲を一覧表示します。 受信すると、ドライバーはこの一覧を返す必要があります、 [ **IRP\_MN\_クエリ\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements) IRP します。 (非 PnP デバイスの基本的な構成は、INF ファイルで記述できます。 デバイスのインストール ソフトウェアを読み取り、INF ファイルと呼び出し、この[構成マネージャーの機能の PnP](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))要件リストを作成する)。

<a href="" id="filtered-configuration"></a>*フィルター選択された構成*  
場合によっては変更をドライバー スタックに指定されているリソースの要件の一覧は、ドライバー スタックへの応答によって返される、 [ **IRP\_MN\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements) IRP します。 PnP マネージャーでは、リソース割り当ての基礎として結果のフィルター選択された構成を使用します。

<a href="" id="override-configuration"></a>*構成をオーバーライドします。*  
基本構成をオーバーライドするリソース要件の一覧。 デバイスの INF ファイルが含まれている場合にデバイス インストーラーが、上書きの構成を作成する通常、 [ **INF DDInstall.LogConfigOverride セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)します。 そのデバイスがシステムから物理的に削除された場合は、上書きの構成は削除されません。

### <a name="logical-configuration-types-for-resource-lists"></a>リソースの一覧の論理構成の種類

<a href="" id="boot-configuration"></a>*ブート構成*  
システムが起動したときに、デバイスのインスタンスに割り当てられているリソースを識別するリソースの一覧。 PnP デバイスは、これは、BIOS で指定された構成 (カードのジャンパによって非 PnP デバイスは、これらのリソースを選択する可能性があります)。受信すると、ドライバーはこのリソースの一覧を返す必要があります、 [ **IRP\_MN\_クエリ\_リソース**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources) IRP します。 (ブート構成できる空にする部分的に BIOS がデバイスで使用されるすべてのリソースを判断できない場合。)PnP マネージャーは、デバイスを削除または再起動された場合、この一覧を変更できます。 デバイスの非 PnP 強制構成ではなく、この構成の種類を使用できます、構成優先順位が低いと同等の構成を強制するよりもがある場合。 デバイス インスタンスごとに 1 つだけのブート構成が存在できます。

<a href="" id="forced-configuration"></a>*変更不可の構成*  
デバイス インスタンスを使用する必要があるリソースを識別するリソースの一覧。 強制の構成では、PnP マネージャーがデバイス インスタンスにその他のリソースを割り当てることを防ぎます。 デバイス インストーラーには、強制されるか、INF に含まれているユーザーから受信した情報に基づいて構成を作成可能性があります。 強制の構成は、そのデバイスがシステムから物理的に削除された場合は削除されません。 デバイス インスタンスごとに 1 つだけの強制構成が存在できます。

<a href="" id="allocated-configuration"></a>*割り当てられた構成*  
デバイス インスタンスによって現在使用されているリソースを識別するリソースの一覧。 デバイス インスタンスごとに 1 つだけ割り当てられた構成が存在できます。

デバイス ドライバーは Irp PnP マネージャーによって送信に対する応答でその情報を返すし、PnP と互換性のあるデバイスの基本的な構成、フィルター選択された構成、およびブート構成を決定するためです。 (詳細については、次を参照してください[PnP デバイスを追加するシステムを実行して](adding-a-pnp-device-to-a-running-system.md)。)。ドライバー ソフトウェアのインストール、構成の強制のオーバーライド構成を作成でき、非 PnP デバイスでは、ブート構成できます。 PnP マネージャーでは、各デバイス インスタンスの割り当てられた構成を保持します。

作成時に、各構成に優先順位が割り当てられます。 PnP マネージャーでは、デバイスのインスタンスに同じ種類の複数の論理構成が割り当てられている検出されると、最初に最高の優先順位で 1 つを使用しようとします。 リソースの競合の場合、その構成は、優先順位の低い [次へ] を使用して構成を試みます。 (構成の優先順位の一覧は、次を参照してください[ **CM\_追加\_空\_ログ\_Conf**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_add_empty_log_conf)。)。

 

 




