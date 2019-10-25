---
title: スレッド、コマンド リスト、および 3-D パイプラインのサポート
description: スレッド、コマンド リスト、および 3-D パイプラインのサポート
ms.assetid: 2c5adc7d-b8ac-48d2-9777-b3d9fbba829a
keywords:
- Direct3D バージョン 11 WDK Windows 7 display、スレッドサポート
- Direct3D バージョン 11 WDK Windows Server 2008 R2 ディスプレイ、スレッドサポート
- Direct3D バージョン 11 WDK Windows 7 display、コマンドリストのサポート
- Direct3D バージョン 11 WDK Windows Server 2008 R2 ディスプレイ、コマンドリストのサポート
- Direct3D バージョン 11 WDK Windows 7 display、3d パイプラインサポート
- Direct3D バージョン 11 WDK Windows Server 2008 R2 ディスプレイ、3d パイプラインサポート
- Direct3D version 11 WDK Windows 7 ディスプレイのスレッドサポート
- Direct3D version 11 WDK Windows Server 2008 R2 のスレッドサポートの表示
- コマンド一覧 Direct3D バージョン 11 WDK Windows 7 ディスプレイのサポート
- tcommand は、Direct3D バージョン 11 WDK Windows Server 2008 R2 ディスプレイのサポートを一覧表示します
- Direct3D version 11 WDK Windows 7 ディスプレイのパイプラインサポート
- Direct3D version 11 WDK Windows Server 2008 R2 ディスプレイのパイプラインサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13e0bc87ad6814f46db8aeda1a3c003a28cbd71d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829374"
---
# <a name="supporting-threading-command-lists-and-3-d-pipeline"></a>スレッド、コマンド リスト、および 3-D パイプラインのサポート


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ユーザーモードの表示ドライバーは、Direct3D version 11 ランタイムがドライバーの[**Getcaps (D3D10\_2)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)関数を呼び出すときにサポートされる新しい direct3d バージョン11の機能 (スレッド、コマンドリスト、3-d パイプラインなど) を示します。 *Getcaps (D3D10\_2)* は、ドライバーが[**D3D10\_2DDI\_adapterfuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体に提供するドライバーのアダプター固有の機能の1つで、 **P\_adapterfuncs**が D3D10DDIARG のメンバーになります。 [ **\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体はを指します。 ドライバーの初期化時にアダプター固有の関数を指定する方法の詳細については、「 [Direct3D バージョン 11 DDI との通信の初期化](initializing-communication-with-the-direct3d-version-11-ddi.md)」を参照してください。 **Getcaps (D3D10\_2)** 関数が呼び出されると、ユーザーモード表示ドライバーは、要求の種類 (D3D10\_2DDIARG の**type**メンバーに指定されている) に基づいて新しい Direct3D バージョン11の機能を提供[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps) *Getcaps (D3D10\_2)* 関数の*PDATA*パラメーターが指す getcaps 構造体。

### <a name="span-idthreading_and_command_listsspanspan-idthreading_and_command_listsspan-threading-and-command-lists"></a><span id="threading_and_command_lists"></span><span id="THREADING_AND_COMMAND_LISTS"></span>スレッド処理とコマンド一覧

Direct3D version 11 API では、アプリケーションスレッドを同期して、1つのスレッドのみが DDI で一度に実行されるようにするための操作モードが必要です。 また、Direct3D version 11 API では、コマンド一覧のソフトウェアエミュレーションを使用した操作モードも必要になります。 これらの操作モードはで必要であり、以前のバージョンの DDIs ( [Direct3D バージョン 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)など) で利用されています。 そのため、ドライバーの作成者向けの開発のために、これらの同じ操作モードが Direct3D バージョン 11 DDI に存在するように拡張されています。 ドライバー作成者は、そのドライバーが Direct3D バージョン 11 DDI 用にサポートする操作のモードを決定できます。

すべてのドライバーは、最終的にすべての種類のスレッド処理操作を完全にサポートする必要があります (つまり、すべてのドライバーは、 [**D3D11DDI\_スレッド化\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_threading_caps)構造体のすべてのスレッド処理機能を最終的にサポートする必要があります)。 ただし、ドライバーでは、API がコマンドリストをエミュレートするか、ドライバーに対してシングルスレッドモードの操作を強制するように要求できます。 Api は、API デバイスの作成時に、DDI デバイスを作成する前に、ドライバーのスレッド処理機能を認識している必要があります。 このため、ランタイムは、ドライバーの[**getcaps (D3D10\_2)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)アダプター固有の関数を[**D3D10\_2DDIARG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps)の**型**メンバーで呼び出すときに、ドライバーのスレッド機能を決定します。 getcaps はに設定され\_D3D11DDICAPS\_スレッド処理。 ドライバーは、ドライバーのスレッド処理機能を識別する D3D10\_2DDIARG\_GETCAPS の**pData**メンバー内にある**D3D11DDI\_スレッド\_CAPS**構造体へのポインターを返します。 ドライバーがコマンドリスト (D3D11DDICAPS\_COMMANDLISTS\_ビルド\_2) もサポートしている場合は、コマンドリストがフリースレッドモードでビルドされるため、ドライバーはフリースレッドモード (D3D11DDICAPS\_フリースレッド) をサポートする必要があります。 ドライバーは、フリースレッドモードとコマンドリストをサポートするためにオプトインする必要があります。 アプリケーションでは、アプリケーションレベルの**Checkfeaturesupport**関数と D3D11\_機能\_スレッド定数として使用することによって、ドライバーが示すサポートを特定できます。ただし、アプリケーションによっては、API によって提供されるサポートによって対処できない場合があります。

### <a name="span-idthree_d_pipeline_levelspanspan-idthree_d_pipeline_levelspan3-d-pipeline-level"></a><span id="three_d_pipeline_level"></span><span id="THREE_D_PIPELINE_LEVEL"></span>3-d パイプラインレベル

Direct3d バージョン 11 ddi をサポートするドライバーは、Direct3D バージョン 11 DDI のすべてのハードウェア機能をサポートするために必要ではありません。 ドライバーは、 [direct3d バージョン 10 ddi](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のみをサポートするハードウェア上にある direct3d バージョン 11 ddi の新しいスレッドモデルをサポートできます。 ランタイムが[**D3D10\_2DDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddiarg_getcaps) Set の**Type**メンバーを使用してドライバーの[**getcaps (D3D10\_2)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getcaps)関数を呼び出すと、Direct3D version 11 runtime によってドライバーの最大ハードウェアレベルが決まります。D3D11DDICAPS を\_します。 ドライバーは、サポートの最大ハードウェアレベルを識別する**D3D10\_2DDIARG\_GETCAPS**の**PData**メンバーの[**D3D11DDI\_3DPIPELINESUPPORT\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_3dpipelinesupport_caps)構造体へのポインターを返します。

Api は、API 機能レベルのサポートのプライマリインジケーターとして、DDI バージョンのみを使用しません。この API を使用すると、ドライバーはこのプロセスに戻ることができます。 ランタイムは、 [**D3D11DDI\_3DPIPELINELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11ddi_3dpipelinelevel)値を選択し、D3D10DDIARG の**Flags**メンバーの一部として、ドライバーの[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しで、デバイスの作成時にその値をドライバーに送り返します。 [**CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体を\_します。

Direct3D バージョン 11 DDI の Direct3D バージョン11より前のハードウェアレベルをドライバーがサポートしている場合、ドライバーの動作には軽微な影響があります。 1つ目の方法として、Direct3D version 11 runtime では、多くの新しい Direct3D バージョン 11 DDI 関数がまったく呼び出されない可能性があります。 たとえば、Direct3D バージョン11ランタイムは、ドライバーが Direct3D バージョン11よりも小さいハードウェア機能レベルをサポートしている場合、新しいシェーダーステージ DDI 関数 ( [**Dssetshader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)など) を呼び出しません。 その他の DDI 関数は、機能レベルの規則に従い、Direct3D バージョン 11 DDI が高い機能に関連付けられている可能性があるという事実を無視します。 たとえば、Direct3D version 11 API の IAVertexInputSlots が32であっても、Direct3D version 10 の機能レベルでは16のみが許可され、ドライバーはこれを想定しています。

非推奨または変換された機能には、もう1つ興味深い側面があります。 廃止は、旧バージョンの DDI 関数を使用する機能をサポートする必要があるため、Direct3D バージョン11の DDI レベルでは使用できません。 たとえば、PIPELINESTATS の Direct3D 11 API バージョンは常に定数です。ただし、異なる[**D3D10\_DDI\_クエリ\_データ\_パイプライン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_ddi_query_data_pipeline_statistics)に要求し、Direct3D 10 の機能レベルと[**D3D11\_ddi\_クエリ\_データ\_パイプラインを使用した統計を\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_ddi_query_data_pipeline_statistics)Direct3D 11 の機能レベルがある統計。 API がテキストフィルターのサイズを廃止しようとした場合でも、ドライバーでは、他の何らかの関数テーブルのエントリを再利用するよりも、DDI 関数テーブルのエントリを完全に廃止することが簡単になります。

Direct3D バージョン 11 DDI をサポートするドライバーが Direct3D バージョン11の全機能レベルをサポートしていない場合でも、「[拡張形式の認識のサポート](supporting-extended-format-awareness.md)」で説明されているように、ドライバーは "拡張形式の認識" を無効にすることはできません。 ドライバーは Direct3D バージョン 11 DDI をサポートするため、ドライバーは次のタスクを処理する必要があります。

-   BGR 形式のサポート

-   XR\_のバイアスサポートを確認するために、 [**Checkformatsupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)関数の呼び出しに正しく応答します。 ドライバーは、サポートを要求するか、サポートを拒否する必要があります。

-   完全に型指定されたバックバッファーのキャストを許可する

また、Direct3D version 11 API は、アプリケーションが複数のスレッドを使用しているかどうかを、D3D11DDI\_CREATEDEVICE\_FLAG\_SINGLETHREADED フラグによってドライバーに通知します。 ドライバーの[**CREATEDEVICE (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しによってディスプレイデバイスが作成されたときに、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体の**Flags**メンバーにこのフラグが存在する場合、ドライバーは遅延がないことを判別できます。同時に作成が行われないため、コンテキストが作成され、ドライバーの同期が不要になります。

 

 





