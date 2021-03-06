---
title: GNSS ドライバーのアーキテクチャ
description: GNSS UMDF 2.0 ドライバーのアーキテクチャ、I/O の考慮事項の概要を説明し、セッションの追跡と修正プログラムのいくつかの型について説明します。
ms.assetid: 11B54F92-DC84-4D74-9BBE-C85047AD2167
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: a27cd96060652aa2d9ae6d662525e3ae0f60b4fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385179"
---
# <a name="gnss-driver-architecture"></a>GNSS ドライバーのアーキテクチャ


GNSS UMDF 2.0 ドライバーのアーキテクチャ、I/O の考慮事項の概要を説明し、セッションの追跡と修正プログラムのいくつかの型について説明します。

## <a name="architecure-overview"></a>アーキテクチャの概要


次の上位レベルのコンポーネントのブロック図では、GNSS UMDF 2.0 ドライバーを Windows 10 プラットフォームと統合する方法を示します。

![ユーザー モード gnss アーキテクチャを示す図](images/gnss-architecture-4.png)

図では、コンポーネントを次に示します。

-   **LBS アプリケーション:** Windows 10 プラットフォームの場所の機能を使用するユーザー アプリケーション

-   **アプリケーションをテストします。** GNSS 機能をテスト用アプリケーション。

-   **GNSS API:** **IGnssAdapter**内部サービスのコンポーネント、場所もアプリケーションをテストする GNSS デバイスの機能を公開する COM (コンポーネント オブジェクト モデル) インターフェイス。 この API の正確な形状は、このドキュメントの範囲外です。 Windows コンポーネントに対するプログラミングによって GNSS デバイスを使用して、 **IGnssAdapter** COM インターフェイスです。 GNSS API セットを唯一の場所のプラットフォーム コンポーネント (たとえば、ロケーション サービスおよびテスト アプリケーションの場所) のプライベート API は、他のファースト パーティまたはサード パーティ製のアプリケーションをご利用いただけません。

-   **GNSS アダプター:** これは、実装するシングルトン COM オブジェクト、 **IGnssAdapter** COM インターフェイスです。 このオブジェクトをインスタンス化しを使用して、GNSS デバイスを使用して、テスト アプリケーションとロケーション サービスの内部コンポーネント、 **IGnssAdapter**インターフェイス。 GNSS 配置エンジン コンポーネント、ロケーション サービスの実装を公開する COM クラス、 **IGnssAdapter**インターフェイス。 ロケーション サービスは、テストするためのファクトリ メカニズムと GNSS アダプター ロケーション サービス内の COM クラスのシングルトンの COM オブジェクトをインスタンス化するためには、他のプロセス外のアプリケーションを公開します。 プロセス外のアプリケーションでは、GNSS ドライバーに対してプログラムへの COM インターフェイス ポインターを使用します。

    > [!NOTE]
    > アプリケーションが処理されるように、COM がプロキシ プロセス外のアプリケーションへのインターフェイス ポインターを処理、 **IGnssAdapter**インプロセス COM オブジェクトが、呼び出しのインターフェイス ポインターがシングルトン GNSS によって処理される実際にはロケーション サービス内でアダプター オブジェクト。

    エンジンの位置づけ GNSS では、内部の GNSS アダプター オブジェクトを使用して、ロケーション サービスを場所固有の機能を提供するためです。 GNSS アダプターが GNSS ドライバーを使用して、ファイル ハンドルを開いて、 **CreateFile** API が適切に GNSS ネイティブ Api 呼び出しをラップし**DeviceIoControl**が、呼び出し、GNSS でステート マシンの管理ドライバーのオブジェクトと上位の層から、さまざまな着信要求の状態を保持します。 このコンポーネントは、このドキュメントで定義されているパブリック GNSS IOCTL インターフェイスを通じて基になる GNSS デバイス スタックと直接対話します。 GNSS デバイスは論理的に、排他リソースとして扱われ、シングルトン GNSS アダプターが GNSS デバイスに対するすべてのアクセスを制御するためです。

    > [!NOTE]
    > 特定のドライバーのホワイト ボックス テスト アプリケーションは、GNSS プライベート Api を通じて GNSS アダプターを使用する代わりに、非運用環境で直接 GNSS ドライバー IOCTL インターフェイスを使用することができますも。 ただし、これらのテスト アプリケーション独自のステート マシンと GNSS アダプターの特定の機能を模倣するために処理を実装する必要があります。



-   **GNSS ドライバー:** UMDF 2.0 を使用して実装されて、IHV 配信のドライバーです。 GNSS ドライバーのサポート、GNSS **DeviceIoControl** GNSS の実際のハードウェアと連動して Api。 GNSS ドライバーは、メディエーター/インテグレーター SUPL 関数としても機能します。

-   **GNSS デバイス/エンジン:** これは、GNSS デバイスの SoC やハードウェアの情報をカプセル化する概念的なコンポーネントです。 IHV は、このコンポーネントは、ので、非常に軽量 GNSS ドライバー レイヤー (基本的に GNSS デバイスとのインターフェイスのアダプター) 内で GNSS 機能のほとんどの実装を選択できます。

## <a name="support-for-gnss-devices-and-drivers-that-follow-the-legacy-windows-model"></a>GNSS デバイスとレガシ Windows モデルに従っているドライバーのサポート


Windows 10 で location プラットフォームは、レガシ センサー v1.0 クラス ドライバーを経由して統合された GNSS デバイスをサポートしています (を参照してください[位置センサー ドライバーを記述](writing-a-location-sensor-driver.md)) によって、新しい統合 GNSS DDI に従ってその[GNSS ドライバー参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver)します。

そのため、Windows 7、Windows 8 および Windows 8.1 に存在していたセンサー v1.0 クラスの拡張機能モデルと統合される GNSS デバイスと Windows デバイスが Windows 10 で変更を必要としない操作を続行するが必要です。 ユーザーのアップグレード処理を向上させるために Windows Update に公開するこれらのドライバー (および、新しいドライバー) を強く推奨します。

GNSS デバイスの Windows 10 で発行されたハードウェア ラボ キット (HLK) でのテストの 2 つの異なるセットもあります。

-   次の新しいモデルのドライバーの認定を受けるテストの 1 つの新しいセット。

-   次の古いモデルのドライバーの認定を受けるテストの別のセット。 これらは、同じ一連の Windows 8.1 で WHCK で使用可能になったテストです。

新しい gatherer コンポーネント、HLK では、存在する場合、システムでは、実行する必要があるテストの 2 つのセットを識別します。

![gnss 2.0 のドライバーとアダプターの通信を示す図](images/gnss-architecture-5.png)

## <a name="coexistence-of-gnss-devices"></a>GNSS デバイスの共存


システムで検出された複数の GNSS デバイスのまれなケース、location プラットフォームはのみを使用して、1 つのデバイス全体を削減するには、主にシステムの電源を消費します。 次の前提条件は検討されました。

-   新しい DDI を使用してデバイスは、新しい、およびそのためより優れた電力消費量がある、複数の有機的のサポート、およびよりサポート可能性が高くする可能性があります。 そのため、古いドライバー モデルを使用してデバイスと、新しいドライバー モデルを使用してデバイスが検出された場合がも、後者が選択されています。

-   内部 GNSS デバイスが存在する場合、ユーザーは外部 GNSS デバイスを接続する場合、は、ユーザーがこの外部デバイスを使用している可能性があります。

これらの前提条件に基づき、location プラットフォームの動作は次のようになります。

-   Coexistent レガシ ドライバーの 2 つのケース:動作には、Windows 8.1、どの両方 GNSS でデバイスを同時に使用して、応答のいずれかと同じでは下位互換性の問題を回避するためにアプリケーションをスタックに伝達されます。

-   1 つの従来のデバイス ドライバーと 1 つの新しいドライバーが外部から接続されている場合:外部から外れている GNSS デバイスが使用されます。

-   デバイスの 1 つの新しいドライバーと 1 つの新しいドライバーが外部から接続されている場合:外部から外れている GNSS デバイスが使用されます。

Geofencing 機能やその他のオフロードされた操作を選択した GNSS デバイスをサポートする場合、オフロードは行われますそのデバイスが使用されます。 機能または複数の GNSS デバイス間でセッション、GNSS アダプターは分割されません。

## <a name="gnss-interface-overview"></a>GNSS インターフェイスの概要

GNSS アダプターと GNSS ドライバー間の相互作用は、次のカテゴリ分類されます。

### <a name="capability-information-exchange"></a>機能の情報交換

Windows プラットフォームで機能拡張と GNSS スタックの適応性をサポートするために、GNSS アダプターと GNSS ドライバー確立によって提供されるサポートと同様に、基になる GNSS スタックの適切に定義されたさまざまな機能の共通の理解、Windows プラットフォームです。 機能面では、この GNSS インターフェイス定義の一部としても Microsoft によって定義され、GNSS 領域でより優れた技術革新が行われ、多様なチップセット/ドライバーのセットが市場に登場も進化します。 GNSS アダプターでは、または、必要に応じての初期化時に基になる GNSS ドライバー/デバイスのさまざまな機能を照会し、それに応じて GNSS ドライバーとの対話を最適化します。

GNSS アダプターと GNSS ドライバーと機能の情報交換を行うコントロールのコードを使用して[ **IOCTL\_GNSS\_送信\_プラットフォーム\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_send_platform_capability)と[ **IOCTL\_GNSS\_取得\_デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_get_device_capability)します。

### <a name="gnss-driver-command-and-configuration"></a>GNSS ドライバー コマンドと構成

GNSS アダプターには、1 回限りの構成または GNSS ドライバーの定期的な再構成を実行できます。 同様に、GNSS アダプターは、ドライバーによって特定 GNSS 固有のコマンドを実行することができます。 これは、ドライバーと高レベルのオペレーティング システム (HLOS) のコマンド実行のプロトコルを定義することで実現されます。 特定のコマンドの種類に応じて、目的とする操作はシステムの再起動後、またはすぐに効果をかかる場合があります。 GNSS デバイス機能の情報と同様に、GNSS コマンドもマイクロソフトによって適切に定義されたこの GNSS インターフェイス定義の一部として、進化将来の技術革新や GNSS デバイス/ドライバーの多様化して続行されます。

デバイス コマンドの実行と構成を行うコントロールのコードを使用して[ **IOCTL\_GNSS\_送信\_DRIVERCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_send_drivercommand)します。

### <a name="position-information"></a>位置情報

これは、基になる GNSS デバイスの主な機能です。 最も基本的なフォームでは、GNSS アダプターは、GNSS ドライバーからデバイスの現在の位置を要求します。 求人要求のバリエーションが含まれます (ただしこれらに限定されません)、次の配置セッションの種類。

-   デバイス (シングル ショット修正プログラム) の現在の位置

-   修正プログラム (時間ベースの追跡) の連続する定期的なストリーム

-   移動のしきい値 (距離ベースの追跡) に基づく修正プログラムの継続的なストリーム

すべての GNSS ハードウェアとドライバーの GNSS で必要な型はシングル ショット唯一の必須の位置のセッションでは、セッションの種類を修正します。 ネイティブ (、SOC、GNSS デバイス、および GNSS ドライバーではなくまたはアプリケーションのプロセッサで実行されているサービスで実装)、時間ベースの追跡セッション、および距離ベースの追跡セッションを必要に応じてサポートできます。 これら 2 つの種類のネイティブの追跡セッションの主な利点は、潜在的な省電力を保持することで、アプリケーションのプロセッサ (AP) 休止時間がかかるの soc 処理の詳細および必要な変更のみが報告されます。 ネイティブ距離ベースの追跡のサポートは、高い省電力を取り込むことができますので、およびアプリケーションはより広い意味で使用するためにネイティブの時間ベースの追跡セッションよりインパクトのあります。

GNSS ドライバーから位置情報を取得するは、次の操作で構成されるステートフルの一意の修正プログラム、セッションを介して行われます。

1.  **修正プログラムのセッションを開始します。** GNSS アダプターは、(LBS アプリケーションからの要求) の結果として開始修正セッションを開始します。 GNSS アダプターは、特定の要件と、要求関連付けの設定を設定し、intimates 制御コードを発行して、修正プログラムを取得するエンジンを起動する GNSS ドライバー [ **IOCTL\_GNSS\_開始\_FIXSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_start_fixsession)します。

2.  **デバイスの位置 (データの修正プログラム) を取得します。** GNSS アダプターが制御コードを問題の修正プログラム、セッションが開始されると、 [ **IOCTL\_GNSS\_取得\_FIXDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_get_fixdata)ドライバーから修正を待ち始めます。 新しい位置情報が、エンジンから利用できる場合、GNSS ドライバーは、この保留中の get 修正プログラムの要求に応答します。

    > [!NOTE]
    > セッションの種類の修正プログラムが LKG 修正プログラム (なく最新の修正プログラム) の場合は、位置情報ドライバーのキャッシュに由来します。

    GNSS アダプターは、非同期 I/O 要求が使用可能な場合は、修正プログラム データを返す GNSS ドライバーの使用可能な常にあることを確認します。 多くの修正プログラム データが予想される場合は、GNSS アダプター (使用して同じ IOCTL) 別の I/O 要求を発行する以上のデータができるまで、このシーケンスが続行されます、修正プログラムまたは修正プログラムの性質によっては、セッションが停止します。

3.  **修正プログラムのセッションを変更します。** GNSS ドライバーがサポートされていない場合、同じ種類の修正プログラムのセッション、GNSS を多重化アダプターが発行する[ **IOCTL\_GNSS\_変更\_FIXSESSION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_modify_fixsession)のそのレベルで多重化時にセッションの種類を修正するとします。

4.  **修正プログラムのセッションを停止します。** GNSS アダプターでは、停止の修正プログラムのセッションと修正プログラムの特定のセッションに関連する詳細の位置情報はありませんが必要なまたは期待を発行します。

### <a name="native-geofencing-support"></a>Geofencing 機能のネイティブ サポート

GNSS DDI には、ジオフェンスの Ioctl この仕様で定義されているセットを使用してシナリオをオフロードがサポートされています。 このサポートを示すため、ドライバーの特別な機能フラグが定義されている、このフラグは、GNSS サポート geofencing 機能をネイティブ スタックする場合にのみ設定する必要があります (つまり実装 geofencing GNSS チップは、アプリケーションのプロセッサではなく)。 ドライバーがジオフェンスがネイティブにサポートしない場合、フラグは設定できません。 HLOS に最適ではないアプリケーションのプロセッサ (AP) が既にサポートしています-ベースのジオフェンス追跡エンジンです。ネイティブ ソリューションができるように最適化された power としてこのソリューションはありませんは、そのため、置き換える必要はありません、アジア太平洋の実装と同じソリューションもテストと最適化です。

> [!NOTE]
> ジオフェンス、HLOS によって、追跡フェンスは損なわれていない場合でも、電源のためドレイン ジオフェンスの侵害を検出するために定期的にスリープをアプリケーションのプロセッサが必要です。 この実装では、最適であると見なされます。

HLOS では、基になるドライバーが信号条件またはネイティブのジオフェンス追跡ソリューションから受信したエラーの通知時に、他の一時的なエラーが原因のジオフェンスを追跡するためにできない場合は、フェールオーバーのメカニズムとして追跡 AP ベースのジオフェンスも使用します。
ジオフェンスの追跡は、SoC を完全に負荷を分散し、アプリケーションのプロセッサがジオフェンス関連のイベントを処理するためだけにウェイク アップしている場合にのみ、geofencing 機能のネイティブ サポートの使用をお勧めします。 GNSS ドライバー、ハードウェアがネイティブのジオフェンスの追跡をサポートしていない場合、ドライバーのレイヤーで実装する読み取ろうとしないでします。

GNSS エンジンは、適切なバランス電源消費量とユーザー エクスペリエンスの検索を有効にする、文書化されている IHV 固有チューニング パラメーターを公開もする必要があります。 サポートされているジオフェンスの数がさらにする必要がありますよりも多く**MIN\_ジオフェンス\_REQUIRED**ヘッダー ファイルで定義されている値。 なお、 **MIN\_ジオフェンス\_REQUIRED** 1 つのアプリケーションにジオフェンスを携帯電話会社または他のアプリケーションによって使用される数の知識があるないので、アプリケーションごとに定義されます。

Geofencing 機能サポートのオフロードにはには、次の要件が含まれます。

-   HLOS DDI 経由で 1 つまたは複数のジオフェンスを作成できるものとし、ドライバーをオフに送信して追跡を開始するためのハードウェア。

-   HLOS は 1 つを削除できるものとまたは DDI 経由でのジオフェンスを以前に作成の詳細はし、ドライバーをオフに送信を追跡することを停止するハードウェア。

-   理想的には、GNSS ハードウェアは各ジオフェンスの状態を追跡する初期のジオフェンスを理解して、この初期状態からのレポートの変更のみを使用する必要があります。 GNSS ハードウェアがこの機能をサポートしていない場合は、ジオフェンスが作成されるたびに、HLOS に初期状態を報告になります。

-   GNSS ハードウェアでは、デバイスの電力効率の高い方法で現在の位置を追跡し、AP スリープ状態、デバイスが入力や、追跡対象のジオフェンスを終了するたびにします。 GNSS ドライバーは、ジオフェンスのアラートを HLOS に渡します。

-   低衛星の信号とその他の一時的なエラー状態では、GNSS エンジンを確実に既存のジオフェンスを追跡することができない可能性があります。 GNSS エンジンは、追跡の中断を検出できるものとし、GNSS ドライバーは、追跡を渡す必要があります、HLOS にエラー アラートの状態。 GNSS ハードウェアが回復し、もう一度ジオフェンスを追跡することまで追跡既定 AP ベースのジオフェンス、HLOS に切り替えます。

-   ジオフェンスを追跡できないことを示す通知を提供する GNSS エンジンが必要な正確な状況はさまざまで、実装は IHV 固有になります。 実装のガイドラインを次に示します。

    -   GNSS エンジンが信頼度の高いユーザーは移行しないと、25 m のジオフェンスの境界がないことを検出できる以下の場合は、GNSS エンジンが追跡エラーを送信する必要はありません。

    -   GNSS エンジンが信頼度の高いユーザーは移行されませんが、25 m のジオフェンスの境界があることを検出できる以下の場合は、GNSS エンジンは 1 分以内に追跡エラーを送信する必要があります。

    -   GNSS エンジンが検出されましたが、ユーザーが移動し、ジオフェンスの境界 100 メートル以内、GNSS エンジンが 1 分以内に追跡エラーを送信する必要があります。

    -   GNSS エンジンが、ユーザーの移動と、100 m のジオフェンスの境界があるかどうかを決定できません。 以下の場合は、GNSS エンジンは 1 分以内に追跡エラーを送信する必要があります。

    -   GNSS エンジンは、ユーザーが移動する検出されましたが場合、GNSS エンジンは、最も近いジオフェンスを時間内に追跡エラー推定の速度の移動距離に比例して送信する必要があります。 内で、エラーを送信する推奨事項は、 \[(Distance-to-closest-fence-boundary(m) 速度 (m/秒) の推定/)-フィフティーン\]します。 GNSS エンジンでは、移動の検出のインジケーターを使用して、追跡のエラーを送信するタイミングを決定します。

    -   GNSS エンジンがユーザーを移動するかどうかを決定できる場合は、GNSS エンジンは、最も近いジオフェンスを時間内に追跡エラーを高速の移動との距離に比例して送信する必要があります。 内で、エラーを送信する推奨事項は、 \[Distance-to-closest-fence-boundary(m)/343(m/s)\]します。

-   GNSS エンジンがジオフェンスの状態エラーの追跡が報告された期間が必要ないジオフェンス、HLOS に送信されるイベントを侵害です。

-   HLOS は、1 つのコマンドでジオフェンスを作成したすべてを削除することによって、追跡、ジオフェンスをリセットできます。

-   コンピューターの再起動またはドライバーの再起動後は、GNSS ハードウェアまたはドライバーのモバイルから配信されたジオフェンスは保持されません。 HLOS エンド ユーザー アプリケーションの代わりに永続化を処理し、必要に応じてジオフェンスを作成または削除します。

GNSS アダプターと追跡の失敗、ジオフェンスの場合、オフロード geofencing 機能をネイティブにサポートする GNSS エンジン間のやり取りの観点からは GNSS アダプターは、次のように実行します。

-   GNSS ドライバーがエラーを追跡するために追跡ベースの AP が使用されます。

-   現在追跡されている OS レベルでもドライバーに同期されるため、ジオフェンスの更新プログラム (追加/削除) のプッシュが継続されます。これにより、どのようなジオフェンスは OS によって現在追跡されているを知る GNSS エンジンと追跡/できない最新のデータに基づく追跡決定が行うことができます。

-   GNSS ドライバーの送信を追跡するには、その機能で成功をバックアップすると、アジア太平洋ベースの追跡ツールによって決定されるジオフェンスの状態の変更をプッシュします。

### <a name="driver-notifications-for-assistance-and-helper-data"></a>アシスタンスとヘルパーのデータのドライバーの通知

ときどき、GNSS ドライバーでは、GNSS アダプターからアシスタンス データまたはヘルパーの操作を必要があります。 サポートするためのユーザーの同意ポップアップ平面配置を開始したユーザー、ネットワークやなど AGNSS データ (時間の挿入、ephemeris、初期の粗い位置) のさまざまなフォームが含まれます。

-   GNSS アシスタンス データは、GNSS アダプターを使用せず、GNSS ドライバーによって取得される可能性があります。 それでも GNSS アダプターを使用して、いくつかの理由からサービスを配置する Microsoft を利用してアシスタンス データが取得されることをお勧めします。

    -   Microsoft の場所スタックはデータ接続を確立するように注意し、ローミング制約、データの基本設定に準拠する quiet モードの統合のネットワークします。

    -   Microsoft のサービスを配置できます定期的にサーバーにバックエンド接続経由で IHV に固有のサポート データを取得し、提供すべてのデバイスにその必要 IHV、世界各地のフロント エンドのサポート サービスをデプロイするための必要性を保存します。可用性、スケーラビリティと応答性の要件を満たします。

-   ユーザーは、アプリケーションがオペレーティング システムによって所有されている受信トレイのプライバシーに関する同意します。 したがって、ネットワークの場所が開始される要求をユーザーに通知する任意の UI またはネットワークに対応するユーザーから同意を要求する UI の場所の要求を開始した、Microsoft によって所有されます。 GNSS アダプターがネットワークの場所の要求の開始を受信し、必要な待機を続行する前に既定の時刻まで、要求を満たすためのユーザーからの応答 GNSS ドライバーに通知します。

GNSS アダプター GNSS ドライバーからこのような要求を積極的に求めていると、それによって、常に 1 つ維持することによって、または保留中の複数の Irp にこの種類の操作を実現できます GNSS ドライバーが、独自の上位レイヤーに要求を開始することができないため、ように GNSS driver は、このような保留中の要求に応答できます。 アシスタンス/ヘルパーの日付の要求の受信後、GNSS アダプター データをフェッチ (GNSS ドライバーに代わって特定のアクションを実行します)、し、その後 GNSS ドライバーは別に必要な情報が挿入**DeviceIoControl**呼び出します。

一般的なイベント モデルを使って、ドライバーからの通知が処理されます。 たとえば、GNSS の詳細については、GNSS アダプターは、コントロール コード[ **IOCTL\_GNSS\_リッスン\_AGNSS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_agnss) GNSS ドライバーから AGNSS 要求を受信します。 GNSS アダプターが AGNSS アシスタンス データとの問題をフェッチ後[ **IOCTL\_GNSS\_挿入\_AGNSS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_inject_agnss) GNSS ドライバーにデータをプッシュします。

この通知メカニズムは、ジオフェンスに関連するアラートのデータとステータスの更新プログラムを受信するためも使用されます。 アダプターは、コントロールのコードを使用して[ **IOCTL\_GNSS\_リッスン\_ジオフェンス\_アラート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_geofence_alert)の受信用個々 のジオフェンスのアラートと[ **IOCTL\_GNSS\_リッスン\_ジオフェンス\_TRACKINGSTATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_geofences_trackingstatus)追跡ジオフェンスの全体的な状態の変更を受信するためです。

### <a name="gnss-driver-logging"></a>GNSS ドライバーのログ記録

診断用には、GNSS ドライバーはエラーとその他の診断情報を以下に示すログ メカニズム (WPP) が規定されている Microsoft または ETW を使用してログインする必要があります。 お勧め、ETW ではなく、ログ目的で、WPP を使用するドライバーの両方のメカニズムがサポートされています。 WPP 推奨される理由は、ドライバーのデバッグに役立つツールの可用性です。

ドライバーは、人間が判読できる、情報をログインしない必要があります。 またはログ記録方法を規定これ以外の場合は、します。 詳細については、次を参照してください。 [WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)します。

WPP ソフトウェア トレースとメッセージのログ記録は、Windows イベント ログ サービスを使用すると似ています。 ドライバーでは、メッセージ ID と書式設定されていないバイナリ データをログ ファイルに記録します。 その後、ポスト プロセッサは、人間が判読できる形式にログ ファイルの情報を変換します。 ただし、WPP ソフトウェア トレースは、可能で、イベント ログ サービスでサポートされているよりも柔軟なメッセージ形式をサポートします。 たとえば、WPP ソフトウェア トレースでは、IP アドレス、Guid、システム Id、タイムスタンプ、およびその他の有用なデータ型の組み込みサポートがあります。 さらに、ユーザーは、そのアプリケーションに関連するカスタム データ型を追加できます。

### <a name="mobile-operator-protocol-support"></a>通信事業者のプロトコルのサポート

IHV 指定 GNSS (GNSS ドライバー、GNSS デバイス/エンジン) スタックはプロトコル (SUPL、UPL、CP など) を配置するさまざまな携帯電話会社をサポートするために必要です。 デバイスが携帯電話会社から受け入れに合格しないと、デバイスを commercialized できる場所を大幅に制限のための手段に失敗しました。

> [!NOTE]
> これらのプロトコルと携帯電話会社の要件の遵守のサポートは、特定のモバイル オペレーター用のデバイスを出荷するために必須です。 通信事業者のプロトコルのサポートは、プラットフォームにモバイル ブロード バンド (MBB) のサポートが含まれていない場合に特別に、電話以外のほとんどのプラットフォームに不可欠な場合があります。

IHV スタックの実装のすべての部分が抽象化されると、Microsoft HLOS コンポーネントに依存しません。
-   (たとえば、プロトコルのしくみ、プロトコルのメッセージの解釈) プロトコルの特定の実装の詳細。

-   実装スタックの形状 (GNSS デバイス/エンジン、または、GNSS ドライバー内で実装が存在できるなど、または個別の HLOS サービスに必要な場合)。

-   プロトコルを実装するための IHV が所有している GNSS スタック内のさまざまな部分の間の相互作用します。 たとえば、GNSS ドライバーは、特定の SUPL プロトコル メッセージに対応することによって行うことができます、Wi-fi スキャンの結果を必要とする場合、ユーザー モード拡張機能 Wi-fi スキャンの結果、プライベートの IOCTL 呼び出しを使用してドライバーを挿入または UMDF 2.0 ドライブのこの部分を作成r、または下位のレベルでは、この操作を処理します。 Microsoft GNSS HLOS コンポーネントは、このような相互作用、IHV GNSS スタック コンポーネントとは無関係です。

要約すると、IHV および OEM 提供する必要が SUPL クライアント (および UPL クライアント システムが中国で出荷される場合) あると/GNSS ドライバー内で統合します。 GNSS DDI を通じて SUPL クライアントと location プラットフォームのすべてのやり取りが行われます。

通信事業者のプロトコルの実装を容易にして、プラットフォーム固有のテクノロジを使用してソフトウェア開発の負荷を軽減には、GNSS アダプターは、IHV GNSS スタックに特定の機能を提供します。 GNSS ドライバーが HLOS コンポーネントからこのような機能を受信するため、仲介者として扱われます、GNSS アダプターが GNSS ドライバーや IHV GNSS スタックの他の部分ではなくのみとどのようにやり取りするなど。 GNSS ドライバー Ioctl では、構文と GNSS ドライバーと GNSS アダプターの間には、このような機能のセマンティクスを定義します。 GNSS ドライバーは、通信事業者のプロトコルを実装する特定の IHV コンポーネントにルーティングします。 幅広く、GNSS アダプター GNSS ドライバーには、次の機能を提供します。

1.  **構成:** モバイルの演算子は、デバイスをプロビジョニングし、OMA プロトコルの標準によって課される構成メカニズムを使用して構成を変更します。 など、UICC に基づいて行うや実行するには、SUPL 構成は必要 SUPL 標準 OMA DM または OMA-CP 経由で取得した SUPL OMA 構成プロファイルの情報を使用します。

    > [!NOTE]
    > (OMA DM と OMA CP) 構成のための電話で利用できる特定の機能は、でした Windows 10 までは他のプラットフォームで使用できます。 すべてのプラットフォームを Windows 10 以降で SUPL 構成 SUPL 構成サービス プロバイダー (CSP) を使用してをサポートできますが、新しいに関して GNSS DDI が使用されます。 挿入、CSP を介したプロビジョニングと、OMA DM または OMA CP を使用して、イメージ自体 (provxml multivariant を通じて) からまたは携帯電話会社からの設定が取得できます。

    Windows 10 では、独自のテクノロジ、解釈し、構成データを抽出用の構成サービス プロバイダー (CSP) を使用したデバイス管理を定義します。 Microsoft では、OMA 構成を使用し、GNSS アダプターを介して GNSS ドライバーへの構成のプッシュの CSP を提供します。

    > [!NOTE]
    > または、IHV も記述できます携帯電話会社を使用するユーザー モード コンポーネント phone に固有のデバイスの管理テクノロジ (Csp) を使用して構成の仕様。 ただし、この IHV で追加の負荷になるし、しないでください。

    1 つだけの SUPL 構成は、デュアル SIM デバイスの場合を含め、システムでサポートされます。 Microsoft は、UICC と UICC 変更に基づいて SUPL を再構成する機能を提供します。 さらに、デバイスのローミングが発生した場合、HLOS 再 SUPL クライアントを構成しますスタンドアロン モードで動作します。 このドキュメントでは、さまざまなモバイル操作プロトコルの場合は、このような構成データをプッシュするための Ioctl を定義します。 (SUPL 1.0 および 2.0 では、v2UPL、など)。

2.  **ユーザーの同意 UI:** プライバシー要件を満たすには、特定のネットワークが開始された配置要求には、ユーザーの同意が必要があります。 Ihv は、プラットフォームのコンポーネント用の UI の作成には使用できません。 そのため GNSS アダプターが GNSS ドライバーに代わって同意をユーザーの UI を処理します。 GNSS ドライバーに対する通知 Ioctl UI ポップアップを要求して、このような要求へのユーザーの応答を伝達するために GNSS アダプターの Ioctl がで定義されている[GNSS ドライバー Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver)します。

完全に機能させる必要があります、IHV スタック SUPL クライアントを実装するためにインターフェイスまたは/OS プラットフォームを通じて使用可能な一般的な機能を使用します。 次は Ihv は、SUPL クライアントを実装するために利用できる Windows 10 で使用できる機能の一覧です。

> [!NOTE]
>  この機能は、location プラットフォームまたは GNSS DDI の一部が含まれていますここでは、わかりやすくするためと SUPL 機能を実装する OS から利用できるものがドライバー開発者向け GNSS を理解します。

![GNSS ドライバーを使用した SUPL クライアントとの対話](images/gnss-architecture-6.png)

-   **SMS ルーター:** SMS ルーターでは、SUPL クライアントで SUPL NI 要求を実行する WAP プッシュの SIP プッシュ メッセージをサブスクライブできるようにします。

-   **接続を構成する接続マネージャーの機能は、このような接続を要求する SUPL と Api の使用は。** 携帯電話会社は、SUPL トラフィック専用の接続、または既定のインターネット接続とは異なる接続だけにする必要があります。 これを行う**接続マネージャー**を提供します。

    -   OEM または携帯電話会社が接続を構成に使用できる構成サービス プロバイダーは SUPL 通信するために使用されます。

    -   SUPL クライアント SUPL 接続の接続パラメーターをクエリするための API です。

    -   前の手順で取得したパラメーターを使用して、SUPL 接続を確立するための API。

-   **携帯ネットワーク接続の構成:** SUPL 接続では、パラメーターなど、さまざまな携帯電話接続のパラメーターを構成するのには、OEM または携帯電話会社が使用できる構成サービス プロバイダー。 この接続に関連付けることができますし、**接続マネージャー** SUPL 目的にします。

-   **SUPL 接続は継続的な接続をアクティブにしておくことを要求します。** SUPL クライアントは、システムでの接続中にスタンバイ、HSLP との接続を開始する必要があります。 これは、GNSS デバイスは、マイクロソフト ベースの配置を使用するように構成するとき、または携帯電話会社、NI 要求を送信するために支援情報を取得する必要があるために発生する可能性があります。 その場合は SUPL クライアントは、HSLP と接続を開始し、SUPL セッションが完了するまで接続がアクティブであることを確認する必要があります。

-   **モバイル ブロード バンド (MBB) モジュールとの対話。** Windows 10 ではありません Api に携帯電話の測定値を取得し、緊急の呼び出しが配置されているときに知っている、HLOS を利用しています。 相互作用を MBB が、MBB と直接統合を実行する必要があります (AT を通じてコマンドやその他の独自のメソッド)。

### <a name="manufacturing-testing"></a>製造のテスト

Oem は、製造時に検証することも、顧客の GNSS ハードウェアと GNSS スタック (GNSS ドライバーおよび GNSS デバイス/エンジン) が正しく動作しているポイントをサポートする必要があります。 IHV は、Oem はこのテストの実行を有効にする独自のメカニズムを提供できます。 または製造テストを開始し、結果を取得する OEM を有効にする DDI で必要に応じて、インターフェイスを実装できます。

場所のフレームワークはバイパスされます製造テストを実施する際にハードウェアの検証またはドライバーの検証に、テストの大きなフォーカスがあること。 一般に、デバイスは、特殊なコンポーネントとサービスの最小限のセットが読み込まれる「オペレーティング システムがセーフ モード」になります。 このモードで、OEM は、一連のテスト_ケースをトリガーするテスト アプリケーションを開始できます。 効率性と製造時の速度は、高する必要があるさまざまなコンポーネント内のテストの同時実行をサポートします。

テストを製造するためのインターフェイスには、2 つの種類テストにはが含まれています。

1.  **通信事業者 wave テスト:** このテストでは、外部接続/アンテナのテストを検証します。 このテスト、GNSS エンジンが CW 信号を検索し、応答で SNRs (信号にノイズ定量) またはキャリア ノイズ比率を測定値を提供する必要があります。 理想的には、テストでは、10 Hz で応答を提供する必要があります。

2.  **自己テストします。** このテストでは、GNSS エンジンの基本機能を検証します。 自己テストできる必要があります (ハードウェアの欠陥、挿入された外部信号を必要とせず、GNSS ハードウェアでの不正な接続エンジンで基本的な問題を検出します。 この検証の目的は、この低コストのテストを行うし、デバイスより徹底的かつ高価なテストを移行する前に、生産ラインのゲートとして使用します。 このテストで、GNSS エンジンとドライバーは暗証番号 (pin) の接続の自己評価を行うし、問題がなければ、または障害が発生したことを示すステータス コードを返します。 エラーが検出されたエラーのエラー コードが示す必要があります。 エラー コードは IHV によって設定されます。

## <a name="io-considerations"></a>I/O に関する考慮事項


GNSS 機能が従来のファイルの読み取りにマップしてのデバイス ドライバーへの書き込み要求していないため、 **ReadFile**と**WriteFile** GNSS driver Api の関数は使用されません。 GNSS 機能は同様に使用して実装するすべての定義 GNSS 固有のデバイスの I/O コントロール (**DeviceIoControl**) Ioctl とも呼ばれる要求。

メソッドを使用して、すべての Ioctl\_入力と出力の両方のデータのデータ転送メカニズムとしてバッファーに格納します。 GNSS に関連するデータのサイズが比較的小さいために、余分なバッファーのコピーは、システム パフォーマンス影響はありません。

使用して、GNSS ドライバーが開かれる、**ファイル\_フラグ\_OVERLAPPED**オプション、 **CreateFile**関数。 そのためすべての Ioctl は暗黙的に非同期です。 ただし、GNSS Ioctl のほとんどは (予想されるドライバーと、結果内のアクティビティが非同期的に戻り、IOCTL トリガーなど) のセマンティクス的に非同期、Ioctl はない論理の意味では意味的に同期非同期アクションまたはこのような Ioctl に関連するアクティビティ。 これらのいくつかの Ioctl の同期の動作を実行した後、GNSS アダプターのスレッドをブロックするだけで実現されます、 **DeviceIoControl** I/O 操作が完了するまでの呼び出し。 そのため、GNSS ドライバーが常にすべての ioctl 処理の一環として、IRP を完了するの責任になります。 だけを優先する GNSS アダプターが期待どおりの同期呼び出しと、エラーが発生した場合、コントラクトの可能性がありますまたはこれらのコマンドを再試行しない可能性があります。 IHV ドライバーは、エラーを返す前に、ドライバーにあるすべてのロジックが組み込まれているかどうかを確認する必要があります。

要求と応答の操作の GNSS アダプターは常に保留中の I/O 操作を使用可能な保留中の IRP 経由 GNSS ドライバーには、前に呼び出した操作に対する応答として送信するデータが含まれている、ときに応答して送信できるようにします。

## <a name="single-shot-session"></a>1 つのスナップショット セッション


ドライバーにシングル ショットの修正プログラムの起動の修正プログラム要求には、正確性と応答時間の値が含まれます。 GNSS エンジンと、アプリケーションの要求の目的を理解し、適切な意思決定を行うこれらの値を使用します。 ドライバーによって、要求が受信されると、エンジンによって生成された中間の修正プログラムを返すことが開始されます。 中間の修正には、修正プログラムの正確性の要件を満たしているか、最終的な修正を計算中にエンジンによって生成されます。 これらの中間の修正プログラムの頻度は強制されません、エンジンの実装の詳細です。 GNSS アダプターには数秒ごとに修正が必要ですが、最後の中間の修正と異なる必要があります。

GNSS エンジンは、最終的な修正プログラムを返す必要があり、後続の計算の実行を停止する、現在の信号条件下でより良い修正プログラムを取得できませんを判断します。 最終的な修正プログラムは、正確性の要件を満たしているか、または、エンジンが現在の条件下で提供される精度を上げることはできませんを示します。

GNSS アダプターでは、2 つのケースのいずれかで 1 つのスナップショット セッションの停止の修正プログラムを発行します。

-   ドライバーから最終的な修正プログラムを取得します。

-   要求の応答時間に達しました。 ここで最後の中間の修正プログラムは、アプリケーションに送信されます。

次の図は、2 つの 1 つショット セッションを示しています。

![中継ぎ局を示す図は、2 つのセッションを修正します。](images/gnss-architecture-7.png)

**セッション 1:** ドライバーは、正確性と応答時間のパラメーターに指定されました。 開始の修正プログラムのコマンドの後に、ドライバーは、中間の修正の送信を開始します。 しばらくすると、最終版としての最後の修正プログラムを示すためより正確な修正プログラムを返すことをできませんでしたが決定されます。 これは、応答時間の制限の到達する前に発生しました。 アダプターでは、最終的な修正プログラムをアプリケーションに送信し、修正プログラムを停止するコマンドを発行します。

**セッション 2:** 同じセッションの 1 つ目のように、この場合、エンジンは、正確性の要件を満たす優れた修正し、保持し、保持を送信する中間を間に修正します。 セッションの応答時間の制限に達すると、アダプターは、ドライバーでは、このセッションを閉じる必要があります停止修正に発行されます。 受信した最後の中間の修正は、アプリケーションに送信されました。

実装の 1 つショットがサポートする場合に考慮すべき重要な設計側面の 1 つは、距離ベースの追跡セッションとセッションの時間ベースの追跡はサポートされている両方でがない場合、GNSS エンジンは続行後 3 ~ 5 秒のサテライトを追跡修正プログラムを停止するコマンドを受信します。 この GNSS アダプターがシミュレートされる距離ベースの追跡セッションを実装する必要があるためやショット 1 つを使用して時間ベースの追跡セッションのセッションを修正する場合、GNSS エンジンのサテライトをすぐに追跡を停止、ほとんどの GNSS デバイス必要があります、不可能の取得での遅延、ナビゲーションのニーズを満たすシミュレートされた追跡セッションを実装する追跡や、アプリケーションのマッピングを実行します。

システム スタンバイ状態の接続はありませんが、システムがアクティブである場合にだけ、GNSS アダプターはシングル ショットの修正プログラムの要求を開始できます。 これは、バック グラウンド タスク、システム サービス、追跡は、アプリケーションのプロセッサまたはそれ以外の場合、ジオフェンスのニーズを満たすために発生する可能性があります。 GNSS ドライバーは、GNSS デバイスにこれらのセッションの要求を渡すことができるものとし、要求を満たすかまたは GNSS アダプターにエラーを提供します。

次のシーケンス図は、スタンドアロンの GNSS 修正の取得に関連する高度なアクションを示しています。 アシスタンス データに対する要求は含まれませんことに注意してください。

![gnss アーキテクチャのシーケンス図 ](images/gnss-architecture-8.png)

シーケンスの説明は次のとおりです。

1.  GNSS アダプターが GNSS ドライバーを使用して、開き、 **CreateFile** API。 GNSS ドライバーを必要な省略可能なコールバックを WDF/KMDF/UMDF になります。 返されたファイル ハンドルは、後続のすべての操作に使用されます。

2.  GNSS アダプターは、さまざまなプラットフォーム機能、ドライバーの通信に IOCTL を発行します。 GNSS ドライバーでは、I/O 操作を完了します。

3.  GNSS アダプターは、デバイスの機能を取得するための IOCTL を発行します。 GNSS ドライバーは、デバイスの機能を返し、I/O 操作を完了します。

4.  GNSS アダプターは、ドライバー固有の構成やコマンドの Ioctl を発行します。 GNSS ドライバーでは、必要なアクションを実行し、I/O 操作を完了します。

5.  GNSS アダプターに関する問題、 [ **IOCTL\_GNSS\_開始\_FIXSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_start_fixsession)パラメーターの型と修正プログラムの他の側面を指定するとします。 この IOCTL の受信後は、GNSS ドライバーは、修正プログラムの受信を開始する基になるデバイスとやり取りし、その後、I/O 操作が完了します。

6.  GNSS アダプターに関する問題、 [ **IOCTL\_GNSS\_取得\_FIXDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_get_fixdata)し、I/O の完了を待ちます。 GNSS ドライバーには、使用可能な中間修正プログラムが含まれている、ときに、I/O 操作を実行してデータを返します。

7.  手順 6 は、GNSS ドライバーでは、これ以上の修正プログラムが予想される (最終的な修正プログラムを受信) であることを示しますまで繰り返されます。

8.  GNSS アダプターに関する問題[ **IOCTL\_GNSS\_停止\_FIXSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_stop_fixsession)します。 GNSS ドライバーでは、元の修正プログラム要求に関連付けられている必要なクリーンアップ操作を行います。

9.  GNSS アダプターは、ドライバー ファイル ハンドルを使用して、閉じ、 **CloseHandle** API。

GNSS Ioctl と関連付けられているデータ構造がで詳しく説明されている、 [GNSS ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/)します。

## <a name="distance-based-tracking-session"></a>距離ベースの追跡セッション


距離ベースの追跡セッションは、.NET Api で使用できる唯一のセッションの種類であったため、これまで、エンド ユーザー アプリケーションでよく使用されます。 距離値は 0 では、GNSS エンジン当事者修正可能な最高のレートでは、ことを示します。

GNSS アダプターは、機能が、後で示す場合にだけ、距離、GNSS ドライバーとのセッションの追跡が起動**SupportDistanceTracking**します。

セッションの追跡の距離のドライバーを開始修正要求には必要に応じて水平方向の精度と球面上の距離は、移動のしきい値が含まれますドライバーをシステムには、GNSS する前に対応するメートル単位で位置の更新プログラムを提供します。 GNSS エンジンは、アプリケーションの要求の目的を理解し、適切な意思決定を行うこれらの値を使用してなどの場所を確認する頻度を適応ことができます。

修正プログラムの開始要求が、ドライバーによって受信されると、最終的な修正プログラムを取得するまでに、エンジンによって生成された中間の修正プログラムを返すことが開始されます。 セッションの最初の位置と見なされます。 この後は、GNSS エンジンが、球面上の距離を約カバーされていたことが検出されたときに修正の提供を開始するものとします。

GNSS エンジンは、そのことはできませんを追跡することがなくなった (たとえば、サテライトが表示されないなくなった場合など) デバイスの場所を判断した場合、エラーを返します GNSS アダプターに location プラットフォームが提供するその他のメカニズムに戻るにことができるようにエンド ユーザー アプリケーションの更新を配置します。 GNSS アダプターは、次の時間内エラーを提供する必要があります。

\[(Distance-remaining-since-last-known-position (m) 速度 (m/秒) の推定/) – 5 秒\]または最大方 5 (秒単位)。

GNSS アダプターにエラーが GNSS エンジンに提供されている場合は、GNSS アダプターではまだ追跡セッションが停止されていません場合は、オン、電源が最適化された方法での場所の追跡を再開できます GNSS エンジンが引き続き必要があります。 IHV は、低電力で、この検出を実行するのに最適化を使用できます。 最適化のための一般的な手法は次のとおりです。

-   プログレッシブ バックオフ

-   再確認するデバイスの動きを示唆している低コストの通知の待機

-   衛星の信号を低電力を確認します

GNSS エンジンがエラー状態の後にもう一度最終的な修正プログラムを提供することと、追跡が正常に再開されたことを示す値としてその位置を GNSS アダプターに送信する必要がありますに。

GNSS アダプターは、追跡セッションが要求をキャンセルまたは新しいアプリケーションで距離を要求しているかどうかに要求した 1 つまたは複数のアプリケーションは、セッションの追跡を基づいている場合は、距離ベースの追跡セッションの変更の修正プログラムのコマンドを発行します。 このような場合は、GNSS は、アダプターは、別のアクティブなセッションを多重化に必要な新しい集計されたセッション パラメーターを計算し、GNSS ドライバーがこれらのパラメーターを更新します。

GNSS アダプターでは、場合に、距離ベースの追跡セッションの修正プログラムを停止するコマンドを発行します。

-   追跡セッションが、システムで使用できるもう 1 つの配置エンジンに渡されました。

-   追跡セッションが要求したアプリケーションには、要求が取り消されました。

次の図は、2 つの距離ベースの追跡セッションを示しています。

![gnss ドライバーの内部の追跡 ](images/gnss-architecture-9.png)

**セッション 1:** GNSS ドライバーには、追跡セッションを開始するときに精度と移動のしきい値のパラメーターを指定されました。 開始の修正プログラムのコマンドの後に、ドライバーは、中間の修正プログラムを送信するまで、最終的な修正プログラムを取得または修正プログラムをこの時点では、このような修正プログラムが GNSS アダプターと GNSS エンジンに提供される精度の要件を満たすまでの距離の追跡プロセスが開始されますを開始します。 セッションがアクティブな間、GNSS アダプターは時の T1 と T2 セッション パラメーターを変更する要求を送信します。 パラメーターの変更されるたびに GNSS ドライバーは GNSS アダプターに修正プログラムの更新を送信し、GNSS アダプターは、修正プログラムを停止するコマンドを送信するまで、新しいパラメーターを使用してセッションを追跡する距離が再開されます。

**セッション 2:** セッション開始のプロセスは、上のセッション 1 に似ていますが、特定の時点に GNSS エンジンは位置を追跡することがありません。 距離と動作の推定の速度に依存している時間が経過 GNSS ドライバーはエラーを送信します。 チェックする低電力を回復できる場合、回復時に新しい修正プログラムを送信することが GNSS アダプターに通知が GNSS エンジンが続行されます。 セッションは、GNSS アダプターは、修正プログラムを停止するコマンドを送信するまで、必要に応じて、新しい修正プログラムで更新されます。

GNSS アダプターは、アクティブにしておくか、システムがコネクテッド スタンバイになって、システムがアクティブなときにだけ中も距離ベースの追跡のセッションの開始可能性があります。 これは、バック グラウンド タスク、システム サービス、追跡は、アプリケーションのプロセッサまたはそれ以外の場合、ジオフェンスのニーズを満たすために発生する可能性があります。 GNSS ドライバーは、GNSS デバイスにこれらのセッションの要求を渡すことができるものとし、要求を満たすかまたは GNSS アダプターにエラーを提供します。

## <a name="time-based-tracking-session"></a>時間ベースの追跡セッション


時間ベースの追跡セッションは、ユーザー インターフェイス (たとえば、およびマップ、ナビゲーションのアプリケーション) を更新する頻度と通常の位置の更新が必要なアプリケーションで使用できます。

GNSS アダプターがセッションの開始時間ベースの追跡 GNSS のドライバーと、後でを示しますが、機能がある場合にのみ**SupportContinuousTracking**します。

必要に応じて水平方向の正確性と優先する時間間隔、時間ベースの追跡セッション用のドライバーを開始修正要求が含まれては GNSS ドライバーを位置の更新プログラムを提供する必要があります。 GNSS エンジンすることをアプリケーションの要求の目的を理解し、適切な意思決定を行うこれらの値を使用してなどの場所の確認、サテライトを提供する、間隔の前に、いくつかの秒の取得を開始する頻度を調整します。タイムリーな更新プログラムを配置します。

修正プログラムの開始要求が、ドライバーによって受信されると、最終的な修正プログラムを取得するまでに、エンジンによって生成された中間の修正プログラムを返すことが開始されます。 セッションの最初の位置と見なされます。 その後、GNSS エンジンはセッション パラメーターに必要な間隔での修正プログラムの提供を開始する必要があります。 GNSS エンジンで、アプリケーションで必要な頻度での位置を提供することがない場合、単に可能な最大レートで修正を提供する必要があります。

GNSS エンジンは、そのことはできませんを追跡することがなくなった (たとえば、サテライトは表示されません)、デバイスの場所を判断した場合、エラーを返します GNSS アダプターに location プラットフォームが位置を提供する他のメカニズムに戻るにことができるようにエンド ユーザー アプリケーションを更新します。

GNSS アダプターにエラーが GNSS エンジンに提供されている場合は、GNSS アダプターではまだ追跡セッションが停止されていません場合は、オン、電源が最適化された方法での場所の追跡を再開できます GNSS エンジンが引き続き必要があります。

IHV は、前のセクションで説明したように低電力は、この検出を有効にするのに最適化を使用できます。 GNSS エンジンがエラー状態の後にもう一度最終的な修正プログラムを提供することと、追跡が正常に再開されたことを示す値としてその位置を GNSS アダプターに送信する必要がありますに。

GNSS アダプターは、追跡セッションが要求をキャンセルまたは新しいアプリケーションが時間ベースの追跡セッションを要求しているかどうかに要求した 1 つまたは複数のアプリケーションの場合、時間ベースの追跡セッションの変更の修正プログラムのコマンドを発行します。 このような場合は、GNSS は、アダプターは、別のアクティブなセッションを多重化に必要な新しい集計されたセッション パラメーターを計算し、GNSS ドライバーがこれらのパラメーターを更新します。

GNSS アダプター場合の時間ベースの追跡セッションを停止する修正プログラム コマンドを問題します。

-   追跡セッションが、システムで使用できるもう 1 つの配置エンジンに渡されました。

-   追跡セッションが要求したアプリケーションには、要求が取り消されました。

次の図は、2 つの時間ベースの追跡セッションを示しています。

![gnss ドライバーの修正プログラムの時間ベースの追跡のダイアグラム](images/gnss-architecture-10.png)

**セッション 1:** GNSS ドライバーには、追跡セッションを開始するときに精度と希望する間隔のパラメーターを指定されました。 最終的な修正プログラムや精度要件を満たしている修正プログラムを取得するまでに、ドライバーが中間の送信を開始するものと開始 fix コマンドが修正 GNSS アダプターに提供されるこのような修正プログラムをポイントして、GNSS エンジン時間ベースの追跡プロセスが開始されます。 セッションがアクティブな間、GNSS アダプターは時の T1 と T2 セッション パラメーターを変更する要求を送信します。 パラメーター、GNSS の変更されるたびに、ドライバーは GNSS アダプターに修正プログラムの更新を送信し、GNSS アダプターは、修正プログラムを停止するコマンドを送信するまでに、新しいパラメーターを使用して、時間ベースの追跡セッションを再開します。

**セッション 2:** セッション開始のプロセスは、上のセッション 1 に似ていますが、特定の時点に GNSS エンジンが停止した位置を追跡できるようにします。 GNSS エンジンは、セッションのパラメーターに必要な間隔の 15 秒以内に修正プログラムを提供することが、GNSS ドライバーはエラーを送信します。 チェックする低電力を回復できる場合、回復時に新しい修正プログラムを送信することが GNSS アダプターに通知が GNSS エンジンが続行されます。 セッションは、GNSS アダプターは、修正プログラムを停止するコマンドを送信するまで、必要に応じて、新しい修正プログラムで更新されます。

GNSS アダプターは、アクティブにしておくか、システムがコネクテッド スタンバイになって、システムがアクティブなときにだけ中にも時間ベースの追跡セッションの開始可能性があります。 これは、バック グラウンド タスク、システム サービス、追跡は、アプリケーションのプロセッサまたはそれ以外の場合、ジオフェンスのニーズを満たすために発生する可能性があります。 GNSS ドライバーは、GNSS デバイスにこれらのセッションの要求を渡すことができるものとし、要求を満たすかまたは GNSS アダプターにエラーを提供します。

## <a name="handle-different-types-of-fix-session-simultaneously"></a>さまざまな種類の修正プログラムのセッションを同時に処理します。


一部の高度な GNSS エンジンは、距離ベースのシングル ショット セッションや時間ベースの追跡セッションを同時に処理できる場合があります。 理想的には独立したセッションする必要がありますには影響しません、互いがこのできない可能性があります常に可能であれば、1 つのショットと時間ベースの追跡の同時セッションの場合は特別に。 このセクションでは、侵害がさまざまな種類の同時セッションの処理にする必要がある場合に、IHV の実装のガイドラインを提供します。

このセクションでは、次の頭字語が使用されます。

-   **SS:** 1 つのスナップショット セッション

-   **により:** 距離追跡ベースのセッション

-   **TBT**:時間ベースの追跡セッション

-   **TBF:** 修正までの時間

次の表は、シングル ショットと時間ベースの追跡セッションを同時に処理するためのいくつかのシナリオを示します。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>ケース</th>
<th>SS はアクティブですか。</th>
<th>アクティブな TBT でしょうか。</th>
<th>ケースの詳細</th>
<th>修正プログラムの許容可能な間隔</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ケース 1</p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>SS セッション時 TBT 定期的なセッションの継続的なが残りのタイムアウトを設定して開始&gt;間隔を =</p></td>
<td><p>TBT 間隔と同じ</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正は、タイムアウトに達するまで送信されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>約間隔に従って受信が修正されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>ケース 2</p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>SS セッション時 TBT 定期的なセッションの継続的なが残りのタイムアウトを設定して開始&lt;間隔</p></td>
<td><p>SS セッションが満たされるまで、間隔、SS タイムアウトとして同じのままにします。</p>
<p>間隔を更新して TBT 間隔と同じであることにし、</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正は、タイムアウトに達するまで送信されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>修正プログラムは、約間隔に従って受信しますが、提供される SS セッション中に頻繁に可能性があります。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>ケース 3</p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>進行中の TBT 定期的なセッションがあるときに開始 SS セッションがタイムアウトで開始&gt;間隔を =</p></td>
<td><p>TBT 間隔と同じ</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正は、タイムアウトに達するまで送信されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>約間隔に従って受信が修正されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>ケース 4</p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>進行中の TBT 定期的なセッションがあるときに開始 SS セッションがタイムアウトで開始&lt;間隔</p></td>
<td><p>SS セッションが満たされるまで、SS タイムアウトと同じにする間隔の変更。 TBT 間隔と同じにする間隔を更新できます。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正は、タイムアウトに達するまで送信されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>修正プログラムは、約間隔に従って受信しますが、提供される SS セッション中に頻繁に可能性があります。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>ケース 5</p></td>
<td><p></p></td>
<td><p>x</p></td>
<td><p>間隔の変更を使い始める TBT 定期的なセッション</p></td>
<td><p>モデムとのセッションは、TBT 間隔と同じであると新しい間隔に更新されます。 モデムのセッションが必要な場合は再起動されます。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>適用なし</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>約間隔に従って受信が修正されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>ケース 6</p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>SS セッションが進行中の TBT 定期的なセッションが受信する残りのタイムアウトの間隔の変更時に継続的な&gt;間隔を =</p></td>
<td><p>TBT 間隔と同じ</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正は、タイムアウトに達するまで送信されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>約間隔に従って受信が修正されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>7 の場合</p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>SS セッションが進行中の TBT 定期的なセッションが受信する残りのタイムアウトの間隔の変更時に継続的な&lt;間隔</p></td>
<td><p>SS セッションが満たされるまで残りのタイムアウト、SS と同じである間隔の変更。 TBT 間隔と同じにする間隔を更新できます。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正は、タイムアウトに達するまで送信されます。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間と最終的な修正が送信されます。</p></li>
<li><p>修正プログラムは、約間隔に従って受信しますが、提供される SS セッション中に頻繁に可能性があります。</p></li>
<li><p>停止が受け取られた直後後にセッションが閉じられます。</p></li>
</ul></td>
</tr>
</tbody>
</table>



同時に時間ベースとの距離ベースの追跡セッションがある場合は、2 つの最小値を使用する追跡 GNSS エンジンの精度を設定できます。 次の表では、同時シングル ショットと追跡セッションがある場合に必要とされる精度の異なる値の大文字と小文字のいくつかのガイドラインも提供します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>ケース</th>
<th>SS 精度</th>
<th>によりまたは TBT 精度</th>
<th>全体的な GNSS エンジンの精度</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ケース 1</p></td>
<td><p>中低--&gt;高</p></td>
<td><p>適用なし</p></td>
<td><p>中低--&gt;高</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新または高精度の結果を取得するには再起動します。 中間の修正プログラムは、利用できるように、HLOS に提供されます。</p></td>
</tr>
<tr class="even">
<td><p>ケース 2</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p>適用なし</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新されるまたは中/低精度の結果を取得するには再起動します。 要件を満たす修正プログラムが既に使用可能なこれが最終的な修正として返されます。 それ以外の場合、中間の修正プログラムは、利用できるよう、HLOS に提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>ケース 3</p></td>
<td><p>中低--&gt;高</p></td>
<td><p>高</p></td>
<td><p>高</p></td>
<td><p><strong>SS セッションの動作:</strong>高精度のセッションを既にがによりまたは TBT セッションが存在すること、SS セッションだけ中間さらに修正プログラムを提供、HLOS に必要な最後の精度を取得または最終的な修正プログラムが取得されるまで。</p></td>
</tr>
<tr class="even">
<td><p>ケース 4</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p>高</p></td>
<td><p>高</p></td>
<td><p><strong>SS セッションの動作:</strong>高精度のセッションを既にがによりまたは TBT セッションが存在すること、SS セッションだけ中間さらに修正プログラムを提供、HLOS に必要な最後の精度を取得または最終的な修正プログラムが取得されるまで。</p></td>
</tr>
<tr class="odd">
<td><p>ケース 5</p></td>
<td><p>中低--&gt;高</p></td>
<td><p>中/低</p></td>
<td><p>中低--&gt;中/低 SS セッションが完了した後に、高</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新または高精度の結果を取得するには再起動します。 中間の修正プログラムは、利用できるように、HLOS に提供されます。</p>
<p><strong>によりまたは TBT セッションの動作:</strong>[Ok] を一時的に高精度の結果が表示されるこのセッションになります。 ただし、SS セッションを提供すると後、は、このセッションの精度が中/低に戻る必要があります。</p></td>
</tr>
<tr class="even">
<td><p>ケース 6</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p>中/低</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新されるまたは中/低精度の結果を取得するには再起動します。 要件を満たす修正プログラムが既に使用可能なこれが最終的な修正として返されます。 それ以外の場合、中間の修正プログラムは、利用できるよう、HLOS に提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>7 の場合</p></td>
<td><p>適用なし</p></td>
<td><p>中低--&gt;高</p></td>
<td><p>中低--&gt;高</p></td>
<td><p><strong>によりまたは TBT セッションの動作:</strong>GNSS デバイスとのセッションが更新または高精度の結果を取得するには再起動します。 中間の修正プログラムは、利用できるように、HLOS に提供されます。</p></td>
</tr>
<tr class="even">
<td><p>8 の場合</p></td>
<td><p>適用なし</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p><strong>によりまたは TBT セッションの動作:</strong>GNSS デバイスとのセッションが更新されるまたは中/低精度の結果を取得するには再起動します。 要件を満たす修正プログラムが既に使用可能なこれが最終的な修正として返されます。 それ以外の場合、中間の修正プログラムは、利用できるよう、HLOS に提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>9 の場合</p></td>
<td><p>高</p></td>
<td><p>中低--&gt;高</p></td>
<td><p>高</p></td>
<td><p><strong>によりまたは TBT セッションの動作:</strong>セッションが高精度の修正プログラムや中間の修正プログラム、変更されないように、既に取得しています。</p></td>
</tr>
<tr class="even">
<td><p>10 の場合</p></td>
<td><p>高</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p>高に変更中/低 SS セッションが完了した後</p></td>
<td><p><strong>によりまたは TBT セッションの動作:</strong>セッションでは、SS セッションが完了するまで高精度の修正プログラムや中間の修正プログラムの取得を続行できます。 中/低精度の修正プログラムを変更ものとします。</p></td>
</tr>
<tr class="odd">
<td><p>11 の場合</p></td>
<td><p>中/低</p></td>
<td><p>中低--&gt;高</p></td>
<td><p>中低--&gt;高</p></td>
<td><p><strong>によりまたは TBT セッションの動作:</strong>GNSS デバイスとのセッションが更新または高精度の結果を取得するには再起動します。 中間の修正プログラムは、利用できるように、HLOS に提供されます。</p></td>
</tr>
<tr class="even">
<td><p>12 の場合</p></td>
<td><p>中/低</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p>高 -&gt;中/低</p></td>
<td><p><strong>によりまたは TBT セッションの動作:</strong>GNSS デバイスとのセッションが更新されるまたは中/低精度の結果を取得するには再起動します。 要件を満たす修正プログラムが既に使用可能なこれが最終的な修正として返されます。 それ以外の場合、中間の修正プログラムは、利用できるよう、HLOS に提供されます。</p></td>
</tr>
</tbody>
</table>










