---
title: スレッド、コマンド リスト、および 3-D パイプラインのサポート
description: スレッド、コマンド リスト、および 3-D パイプラインのサポート
ms.assetid: 2c5adc7d-b8ac-48d2-9777-b3d9fbba829a
keywords:
- Direct3D バージョン 11 WDK Windows 7 の表示、スレッドのサポート
- Direct3D バージョン 11 WDK Windows Server 2008 R2 表示は、スレッドのサポート
- Direct3D のバージョン 11 WDK Windows 7 の表示、コマンドを一覧表示のサポート
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示、コマンドを一覧表示のサポート
- Direct3D のバージョン 11 WDK Windows 7 表示、3-D のパイプラインのサポート
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 表示、3-D のパイプラインのサポート
- スレッドの Direct3D のバージョン 11 WDK Windows 7 の表示のサポート
- スレッドの Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示のサポート
- コマンドには、Direct3D のバージョン 11 WDK Windows 7 の表示のサポートが一覧表示します
- tcommand のリストをサポートする Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示
- Direct3D のバージョン 11 WDK Windows 7 のディスプレイのパイプラインのサポート
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示用のパイプラインのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c5984748274c8a2e0e418df5ce4177959e6a4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350115"
---
# <a name="supporting-threading-command-lists-and-3-d-pipeline"></a>スレッド、コマンド リスト、および 3-D パイプラインのサポート


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

ユーザー モードのディスプレイ ドライバーがサポートされる新しい Direct3D バージョン 11 の機能を示します (たとえば、スレッド、コマンド リスト、および 3-D パイプライン)、Direct3D のバージョン 11 ランタイムが、ドライバーを呼び出すときに[ **GetCaps(D3D10\_2)** ](https://msdn.microsoft.com/library/windows/hardware/ff566764)関数。 *GetCaps (D3D10\_2)* で、ドライバーには、ドライバーのアダプター固有の関数の 1 つ、 [ **D3D10\_2DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541900)構造体、 **pAdapterFuncs\_2**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)へのポインターを構造体します。 ドライバーの初期化中にアダプターに固有の機能を提供する詳細については、次を参照してください。 [Direct3D のバージョン 11 DDI との通信を初期化して](initializing-communication-with-the-direct3d-version-11-ddi.md)します。 ときにその**GetCaps (D3D10\_2)** 関数が呼び出されると、ユーザー モードのディスプレイ ドライバーが、要求の種類に基づいて、新しい Direct3D バージョン 11 の機能を提供します (で指定される、**型**メンバー、 [ **D3D10\_2DDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff541887)構造体、 *GetCaps (D3D10\_2)* 関数の*pData*パラメーターが指す) です。

### <a name="span-idthreadingandcommandlistsspanspan-idthreadingandcommandlistsspan-threading-and-command-lists"></a><span id="threading_and_command_lists"></span><span id="THREADING_AND_COMMAND_LISTS"></span> スレッド処理とコマンドの一覧

Direct3D のバージョン 11 API では、1 つのスレッドだけが一度に DDI でが実行されるようにするアプリケーションのスレッドを同期する操作のモードが必要です。 Direct3D のバージョン 11 API には、コマンド一覧のソフトウェア エミュレーションの動作モードも必要です。 これらの操作モードに必要なし、Ddi の前のバージョンで利用 (次のように、 [Direct3D のバージョン 10 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552909))。 そのため、ドライバー作成者、開発の支援として、これらの同じモードの操作は、11 DDI Direct3D のバージョンで存在に拡張されます。 操作のどのモード、Direct3D のバージョン 11 をサポートするためには、そのドライバーを希望ドライバー作成者が決定できます DDI します。

すべてのドライバーが操作スレッド処理のすべての種類をサポートする必要があります最終的に完全に (つまり、すべてのドライバーにはのすべてのスレッド処理機能がサポートする最終的に、 [ **D3D11DDI\_スレッド処理\_CAP**](https://msdn.microsoft.com/library/windows/hardware/ff542163)構造)。 ただし、ドライバーでは、API がコマンド一覧をエミュレートまたはドライバーの動作をシングル スレッド モードを適用することを要求できます。 API は、DDI デバイスを作成する前に、API、デバイスの作成時に、ドライバーのスレッド処理の機能の対応である必要があります。 したがって、ランタイムは、ドライバーは、ドライバーを呼び出すときに、機能のスレッドを決定[ **GetCaps (D3D10\_2)** ](https://msdn.microsoft.com/library/windows/hardware/ff566764)とアダプター固有の関数、**型**のメンバー [ **D3D10\_2DDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff541887) D3D11DDICAPS に設定\_スレッド処理します。 ドライバーへのポインターを返します、 **D3D11DDI\_スレッド処理\_CAP**構造体、 **pData** D3D10 のメンバー\_2DDIARG\_GETCAPS ですドライバーのスレッド処理の機能を識別します。 ドライバーは、フリー スレッドのモードをサポートする必要があります (D3D11DDICAPS\_FREETHREADED) ドライバーには、コマンド一覧もサポートしている場合 (D3D11DDICAPS\_COMMANDLISTS\_ビルド\_2) コマンドでビルドを一覧表示するため、フリー スレッドモード。 ドライバーする必要がありますで、シングル スレッド モードをサポートすると、コマンドのリスト。 アプリケーションは、アプリケーション レベルを使用して、ドライバーを示すサポートを確認できます**CheckFeatureSupport**関数と、D3D11\_機能\_スレッド処理の定数ですただし、いくつか。アプリケーションは、API が提供するサポートのためされてもかまわない。

### <a name="span-idthreedpipelinelevelspanspan-idthreedpipelinelevelspan3-d-pipeline-level"></a><span id="three_d_pipeline_level"></span><span id="THREE_D_PIPELINE_LEVEL"></span>3-D パイプライン レベル

11 DDI は Direct3D のバージョン 11 のすべてのハードウェア機能をサポートする必要はありません、Direct3D のバージョンをサポートするドライバー DDI します。 Direct3D のバージョン 11 の新しいスレッド処理モデルをサポートできるドライバーのみをサポートするハードウェア上に DDI、 [Direct3D のバージョン 10 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552909)します。 Direct3D のバージョン 11 ランタイム ランタイムが呼び出す、ドライバーの場合、ドライバーのハードウェアの最大レベルのサポートを決定します[ **GetCaps (D3D10\_2)** ](https://msdn.microsoft.com/library/windows/hardware/ff566764)関数と、 **型**のメンバー [ **D3D10\_2DDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff541887) D3D11DDICAPS に設定\_3DPIPELINESUPPORT します。 ドライバーへのポインターを返します、 [ **D3D11DDI\_3DPIPELINESUPPORT\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff542134)構造体、 **pData**のメンバー **D3D10\_2DDIARG\_GETCAPS**サポートのハードウェアの最大レベルを識別します。

API が API の機能のレベルのサポート; のプライマリ インジケーターとして DDI バージョンのみを使用しません。API は、このプロセスにフィードバックするドライバーを使用します。 ランタイムの選択、 [ **D3D11DDI\_3DPIPELINELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff542126)値、およびフィード値に戻す、ドライバー、ドライバーの呼び出しでデバイスの作成中に[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)の一部として、関数、**フラグ**のメンバー、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)構造体。

ドライバーがサポートしている場合は、ハードウェア レベル 11 DDI を Direct3D のバージョンの Direct3D のバージョン 11 より小さい、ドライバーの動作に軽微な影響があります。 最初は、Direct3D のバージョン 11 ランタイム可能性があります多くの新しい Direct3D のバージョン 11 DDI 関数をまったく呼び出しすることはないことです。 たとえば、Direct3D のバージョン 11 ランタイムは呼び出しません新しいシェーダー ステージのいずれか DDI 関数 (など[ **DsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff557305)) ドライバーは、Direct3D 未満であるハードウェア機能レベルをサポートしている場合バージョン 11。 他の DDI 関数は、機能レベルの規則に従うし、こと、Direct3D バージョン 11 DDI 可能性があります高い機能に関連付けられているという事実が無視します。 など、IAVertexInputSlots Direct3D のバージョン 11 api は、32、Direct3D のバージョンの 10 の機能レベルでは、16 のみが許可し、は、ドライバーが期待する必要があります。

非推奨と変換後の機能は、もう 1 つの興味深い側面を紹介します。 非推奨となるはできません、Direct3D のバージョン 11 DDI レベルで廃止が DDI 関数の以前のバージョンの express 機能をサポートする必要があります。 たとえば、PIPELINESTATS の direct3d11 API バージョンは常に定数;ただし、異なる要求[ **D3D10\_DDI\_クエリ\_データ\_パイプライン\_統計**](https://msdn.microsoft.com/library/windows/hardware/ff541972) direct3d10 機能レベルと[ **D3D11\_DDI\_クエリ\_データ\_パイプライン\_統計**](https://msdn.microsoft.com/library/windows/hardware/ff542171) direct3d11 の機能レベルなどなど。 場合でも、API では、フィルターのテキストのサイズを廃止しようとして、DDI 関数テーブル エントリの他の情報を関数のテーブルのエントリを再利用しようとするよりも、全体を廃止するドライバーを簡単になります。

11 DDI は完全な Direct3D バージョン 11 の機能レベルをサポートしていません、Direct3D のバージョンをサポートしているドライバー、ドライバーできませんオプトアウト「形式の拡張の認識」」の説明に従って場合でも[拡張形式の認識をサポートしている](supporting-extended-format-awareness.md)します。 ドライバーは、Direct3D のバージョン 11 をサポートしているため DDI、ドライバーは、次のタスクを処理する必要があります。

-   BGR 形式をサポートします。

-   呼び出しに正しく応答その[ **CheckFormatSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff539390) XR をチェックする関数\_バイアス サポートします。 ドライバーは、する必要がありますか、サポートを要求またはサポートを拒否します。

-   型指定された完全にバック バッファーのキャストを許可します。

Direct3D のバージョン 11 API もドライバーに通知、アプリケーションが、D3D11DDI による複数のスレッドを使用するかどうか\_CREATEDEVICE\_フラグ\_シングル ・ スレッドのフラグ。 このフラグに存在する場合、**フラグ**のメンバー、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)を呼び出すことによって、ディスプレイ デバイスが作成されたときに、ドライバーの[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)関数の場合、ドライバーしたことを確認コンテキストの遅延は作成されませんを作成して同期を同時に、ドライバーが必要ないことはありません発生します。

 

 





