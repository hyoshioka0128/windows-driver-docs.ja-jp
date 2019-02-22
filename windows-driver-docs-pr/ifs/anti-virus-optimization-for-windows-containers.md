---
title: Windows コンテナーのウイルス対策の最適化
description: このトピックでは、ウイルス対策製品は Windows コンテナー内で実行するときに利用できる最適化について説明します。
ms.assetid: 101BC08B-EE63-4468-8B12-C8C8B0E99FC5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b5552ba5db2b5e4ad041ecf2d07e382238d0af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557588"
---
# <a name="span-idifskanti-virusoptimizationforwindowscontainersspananti-virus-optimization-for-windows-containers"></a><span id="ifsk.anti-virus_optimization_for_windows_containers"></span>Windows コンテナーのウイルス対策の最適化


**適用対象します。**
-   Windows 10 Version 1607
-   Windows Server 2016
-   ホストで実行されているウイルス対策製品

このトピックでは、ウイルス対策製品は Windows コンテナーのファイルの重複をスキャンしないようにするために利用でき、コンテナーの起動時間を向上させるための最適化について説明します。

## <a name="span-idcontaineroverviewspanspan-idcontaineroverviewspanspan-idcontaineroverviewspancontainer-overview"></a><span id="Container_overview"></span><span id="container_overview"></span><span id="CONTAINER_OVERVIEW"></span>コンテナーの概要


Windows コンテナー機能は、配布とアプリケーションの配置を簡単に設計されています。 詳細についてはの概要を参照してください。 [Windows コンテナー](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)します。

コンテナーは、複数のパッケージのレイヤーから構築されます。 Windows ベース OS パッケージは、最初の層を形成します。

各コンテナーにはそのコンテナーのシステム ボリュームを表すボリュームを分離します。 コンテナーの分離のフィルター (**wcifs.sys**) 仮想のオーバーレイのこのコンテナーのボリューム上にパッケージのレイヤーを提供します。 オーバーレイは、プレース ホルダー (再解析ポイント) を使用して実現されます。 コンテナーは、overlain のパスを最初にアクセスする前に、プレース ホルダーを含むボリュームがシード処理します。 ファイルはパッケージ ファイルに送られますプレース ホルダーを読み取ります。 この方法で同じ基になるパッケージ ファイルのデータ ストリームを複数のコンテナーのボリュームにアクセスできます。

コンテナーが、ファイルを変更した場合、分離のフィルターはコピー オン ライトを実行し、パッケージ ファイルの内容と、プレース ホルダーを置き換えます。 これにより、その特定のコンテナーのパッケージ ファイルに「リンケージ」が中断します。

## <a name="span-idreadredirectionspanspan-idreadredirectionspanspan-idreadredirectionspanread-redirection"></a><span id="Read_redirection"></span><span id="read_redirection"></span><span id="READ_REDIRECTION"></span>読み取りのリダイレクト


プレース ホルダー ファイルからの読み取りは、分離フィルターによって、適切なパッケージのレイヤーにリダイレクトされます。 リダイレクトは、フィルターのレベルで実行されます。 フィルターでは、下記の AV 範囲であるために、AV フィルターでは、読み取りのリダイレクトは表示されなくなります。 AV にも、リダイレクトを設定するために実行するパッケージ ファイルの開き表示されなくなります。

AV、フィルターでは、コンテナーのシステム ボリューム上のすべての操作の完全なビューが。 プレース ホルダー ファイルだけでなく、ファイルの変更または新しいファイルの追加の操作が表示されます。

## <a name="span-idredundantscanningproblemspanspan-idredundantscanningproblemspanspan-idredundantscanningproblemspanredundant-scanning-problem"></a><span id="Redundant_scanning_problem"></span><span id="redundant_scanning_problem"></span><span id="REDUNDANT_SCANNING_PROBLEM"></span>冗長なスキャンの問題


多くのコンテナーと同じパッケージのレイヤーによって可能性あります。 特定のパッケージ ファイルの同じデータ ストリームは複数のコンテナーのシステム ボリューム上のプレース ホルダーのデータを提供します。 その結果はすべてのコンテナー内の同じデータの冗長のウイルス対策スキャンの潜在的です。 これは、コンテナーのパフォーマンスに不要なマイナス影響を与えます。 これは、コンテナーは短時間で起動する必要があり、有効期間が短い場合がありますを signification コストです。

## <a name="span-idrecommendedapproachspanspan-idrecommendedapproachspanspan-idrecommendedapproachspanrecommended-approach"></a><span id="Recommended_approach"></span><span id="recommended_approach"></span><span id="RECOMMENDED_APPROACH"></span>推奨されるアプローチ


コンテナーの冗長なスキャンを回避するためには、ウイルス対策製品が以下に示すように、その動作を変更することをお勧めします。 このアプローチの顧客のリスク/reward メリットを判断するウイルス対策製品の責任です。 詳細については、次を参照してください。[メリットとリスク](#benefits-risks)します。

### <a name="span-id1packageinstallspanspan-id1packageinstallspanspan-id1packageinstallspan1-package-install"></a><span id="1._Package_install"></span><span id="1._package_install"></span><span id="1._PACKAGE_INSTALL"></span>1.パッケージのインストール

パッケージのインストール中に、管理ツールのレイヤーのルートの下のパッケージ内のファイルはレイアウトします。 AV フィルターは、パッケージのルートに配置されているが、通常と同じように、ファイルをスキャンする続行する必要があります。 これにより、マルウェアに関しては、最初のレイヤー内のファイルすべてをクリーンアップします。

### <a name="span-id2containstartandexecutionspanspan-id2containstartandexecutionspanspan-id2containstartandexecutionspan2-container-start-and-execution"></a><span id="2._Contain_start_and_execution"></span><span id="2._contain_start_and_execution"></span><span id="2._CONTAIN_START_AND_EXECUTION"></span>2.コンテナーの開始と実行

コンテナーのボリュームのリアルタイム スキャン、AVs は冗長性を回避するようにスキャンする必要があります。 プレース ホルダー ファイルには、特別な考慮が必要があります。 冗長なスキャンが問題にならないように、コンテナーまたはコンテナーで作成された新しいファイルが変更されたファイルはリダイレクトされません。

冗長なスキャンを避けるためには、AV フィルターはコンテナーのボリュームとそれらのボリュームにプレース ホルダーを識別するためにまず必要があります。 さまざまな理由は、ボリュームがコンテナーのボリュームの場合、または指定されたファイルがプレース ホルダー ファイルの場合にクエリを実行するウイルス対策フィルターの直接的な方法はありません。 分離フィルターには、アプリケーション互換性の理由から (一部のアプリケーションは正常に動作しない再解析ポイントへのアクセスは対応している場合) のプレース ホルダーの再解析ポイントが非表示にします。 また、ボリューム コンテナーの実行中にコンテナーのボリュームだけとは。 コンテナーを停止する可能性があり、ボリュームを再マウントに残ることがあります。 代わりで事前に作成、AV フィルターは、コンテナーのコンテキストで開いているかどうかを決定するファイル オブジェクトを照会する必要があります。 アタッチできますし、および作成する ECP と作成の完了時にプレース ホルダーの状態を受信します。

次の変更は、ウイルス対策製品が必要であります。

-   **中には、事前にコンテナーのボリュームの作成をプレース ホルダーの情報を受け取る作成ここに、ECP をアタッチします。** これらの作成を使用して、fileobject からサイロのパラメーターをクエリすることによって識別できます**IoGetSiloParameters**します。 フィルターのサイズを指定する必要があります、 **WCIFS\_リダイレクト\_ECP\_コンテキスト**構造体。 その他のすべてのフィールドでは、ECP が受信確認される場合は、設定のフィールドです。

-   **後を作成する場合は、応答が、ECP ECP リダイレクトのフラグを確認します。** スクラッチ ルート (新しいまたは変更されたファイル) から、またはパッケージのレイヤーから、オープンが処理されるかどうか、フラグが示されます。 フラグは、パッケージの層が登録されている、リモートであるかどうかも示します。

    -   リモートのレイヤーからサービスが提供されるが開いたら、AV は、ファイルのスキャンをスキップする必要があります。 これは、リダイレクトのフラグで示されます。

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER && WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REMOTE_LAYER`

        リモートのレイヤーでは、リモート ホストでのスキャンが完了と見なさ ことができます。 HYPER-V コンテナーのパッケージは、ユーティリティ、コンテナーをホストする VM にリモートです。 これらのパッケージは、SMB 経由で VM のループバック ユーティリティによってアクセスされるときに、HYPER-V ホストで通常スキャンされます。

        リモート経由での VolumeGUID、FileId が適用されませんので、これらのフィールドは設定できません。

    -   登録されているレイヤーからサービスが提供されるが開いたら、AV は、ファイルのスキャンをスキップする必要があります。 これは、リダイレクトのフラグで示されます。

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER        &&  WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REGISTERED_LAYER`

        登録済みの層は、パッケージのインストール中に、署名の更新後非同期的にスキャンする必要があります。

        **注**  登録されているレイヤー識別できない、システムによって、将来します。 この場合、ファイルのローカル層する必要があります個別として識別されることの最後の項目で説明されています。

         

    -   ローカル パッケージのレイヤーからサービスが提供されるが開きの AV する必要がありますと使用して、指定された VolumeGUID FileId レイヤー ファイルの特定、ファイルをスキャンする必要があるかどうか。 ボリュームの GUID と FileId によってインデックス付けされたスキャン済みファイルのキャッシュを作成するアクセス違反が必要になります可能性があります。 これは、リダイレクトのフラグで示されます。

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER`

    -   スクラッチ場所にファイルを新しい/変更、ウイルス対策製品がファイルをスキャンし、通常その修復を実行する必要があります。 これは、リダイレクトのフラグで示されます。

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_SCRATCH`

        ないためレイヤー ファイルここで、VolumeGUID と FileId は設定できません。

-   **ストリームのコンテキストで永続的なマーカーとして、「このファイルはレイヤーからサービス」を保存しません。** 作成した後、レイヤーのルートからサービスが最初にファイルを変更できます。 この場合、同じファイルの後続の作成は、コンテナーのボリュームから作成のサービスを受けること可能性があります。 AV フィルターは、これは発生を理解する必要があります。

## <a name="span-iddontusethelayerrootlocationsregistrykeyspanspan-iddontusethelayerrootlocationsregistrykeyspanspan-iddontusethelayerrootlocationsregistrykeyspandont-use-the-layerrootlocations-registry-key"></a><span id="Don_t_use_the_LayerRootLocations_registry_key"></span><span id="don_t_use_the_layerrootlocations_registry_key"></span><span id="DON_T_USE_THE_LAYERROOTLOCATIONS_REGISTRY_KEY"></span>LayerRootLocations のレジストリ キーを使用しないでください。


以前は、お勧めしますを使用して、`LayerRootLocations`基本イメージの場所を取得するレジストリ キー。 AV 製品では、このレジストリ キーが使用できなくする必要があります。 代わりに、このトピックの「推奨されるアプローチを使用して、冗長スキャンしないようにします。

登録パッケージのレイヤーに使用されていたレジストリの場所:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Virtualization\LayerRootLocations`

## <a name="span-idbenefits-risksspanspan-idbenefits-risksspanbenefits-and-risks"></a><span id="benefits-risks"></span><span id="BENEFITS-RISKS"></span>メリットとリスク


次の利点とウイルス対策製品にこれらの新しい最適化を使用するリスクを検討してください。

### <a name="span-idbenefitsspanspan-idbenefitsspanspan-idbenefitsspanbenefits"></a><span id="Benefits"></span><span id="benefits"></span><span id="BENEFITS"></span>利点があります。

-   コンテナーの開始または (最初のコンテナー) に対しても実行時間に影響はありません。
-   複数のコンテナーで同じコンテンツのスキャンを回避できます。
-   Windows Server のコンテナーに対して機能します。 HYPER-V コンテナーは、このパッケージの動作しますが、コンテナーの実行の追加の作業が必要です。 

### <a name="span-idrisksspanspan-idrisksspanspan-idrisksspanrisks"></a><span id="Risks"></span><span id="risks"></span><span id="RISKS"></span>上のリスク

コンテナーが起動された場合、署名の間に更新し、次回のスケジュールされた事前対応型のマルウェア対策スキャン、コンテナー内で実行ファイルが最新のマルウェア対策シグネチャに関してスキャンされません。 このリスクを軽減するためにされていないが、署名の更新プログラム事前対応型の前回のスキャン後場合にのみ、ウイルス対策製品はリダイレクトされたファイルのスキャンをスキップする可能性があります。 最新のシグネチャでプロアクティブなスキャンが完了するまでこの制限コンテナーのパフォーマンスが低下します。 必要に応じて、ウイルス対策製品は、後続のコンテナーの起動がより効率的になるよう、このような状況でプロアクティブなスキャンをトリガーできます。

 

 




