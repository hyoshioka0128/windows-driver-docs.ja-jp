---
title: ドライバーの配布を Windows のバージョンに基づいて制限または拡張する方法
description: ドライバーの配布を変更するために、ドライバー申請の下限や上限を作成します。
ms.topic: article
ms.date: 06/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: be0a92b0c9d72640b4dfaf615be8d8dc35cbb1a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364463"
---
# <a name="how-to-limit-or-expand-a-drivers-distribution-based-on-windows-version"></a>ドライバーの配布を Windows のバージョンに基づいて制限または拡張する方法

パートナーは、ドライバーの OS 配布申請を拡張または制限することが必要になる場合があります。  このトピックでは、これに対する各関連出荷ラベル機能とそれらの使用方法について説明します。

## <a name="important-information"></a>重要情報

これらの機能の使用を開始する前に、いくつかの重要な原則、用語、定義について理解し、留意する必要があります。

**Windows Update**:ドライバーを RS1 (Windows 10、バージョン 1607) などの特定の OS リリースに公開すると、Windows Update によって、RS2、RS3、およびそれ以降 (Windows 10、バージョン 1607、1703、および 1709) を実行しているシステムにもドライバーが提供されます。 しかし、TH1 または TH2 (Windows 10 バージョン 1507 または 1511) には提供されません。 つまり、ドライバーは常に "*将来に向かって提供*" されます。
これは、出荷ラベルの PNP グリッド内で OS とハードウェアの ID の組み合わせを扱うときに覚えておくことが特に重要です。 実際には、将来に向かったドライバー提供は、前の例では RS2 と RS3 の両方に同じハードウェア ID を発行する必要がないことを意味します。 Windows Update では、RS2 以降のバージョンに RS1 ポスティングが提供されます。  PNP グリッド内で対象にする最小 OS リリースにのみ発行する "*必要があります*"。

**動的更新と OS の下限**:Windows **アップグレード** プロセス中に Windows Update が呼び出されると、クライアントによって報告された現在の OS バージョン情報を上書きするための特別なロジックが使用され、対象機能の更新バージョンに設定されます。 たとえば、クライアントが 10.0.17763 (Windows 10、バージョン 1809) 上にある場合に、10.0.18362 (Windows 10、バージョン 1903) にアップグレードすると、動的更新では 18362 OS 境界内からドライバーが提供されます。 これは、下限機能を使用するときに理解することが特に重要です。 詳しくは、「[ドライバーの配布に関する Windows Update の自動規則とオプション規則について](understanding-windows-update-automatic-and-optional-rules-for-driver-distribution.md)」をご覧ください。

**申請の所有者**:HLKx または .CAB ドライバー パッケージの元の申請者。  開始者は、ドライバーの拡張機能の使用を許可されます。  "*共有申請*" の受信者は、一部の機能について申請の所有者と連携する必要があります。

**必要なアクセス許可**:管理者、出荷ラベルの所有者、および出荷ラベルのプロモーターとして指定されたユーザーだけが、ドライバー申請の下限と上限を設定できます。  また、共同エンジニアリング パートナーだけが、上限ベースとビルド番号ベースの機能にアクセスできます。

**下限と上限の種類**:ドライバー ダッシュボードでサポートされている下限と上限には、次の 2 つの種類があります。

<table>
  <thead>
    <tr>
      <th>下限/上限の種類</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>OS リリース ベース</td>
        <td>
        <ul>
            <li>選択肢は、TH、RS1、RS2 などに制限されます。</li>
            <li>一般向けにリリースされるドライバー用の下限/上限の種類です。</li></ul>
        </td>
    </tr>
    <tr>
      <td>ビルド番号ベース</td>
      <td>
        <ul>
            <li>"<em>Microsoft の共同エンジニアリング パートナーのみが利用できます。</em>"</li>
            <li>選択肢は、リリースされた最新の Windows バージョンよりも大きい 5 桁のビルド番号に制限されます。</li>
            <li>リリースされていないバージョンの Windows 用にドライバーを開発するときに使用されます。</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## <a name="setting-an-os-floor"></a>OS の下限の設定

* "*下限は、PnP グリッドからハードウェア ID と OS の組み合わせを選択したときに、暗黙的かつ自動的に設定されます。* " つまり、PnP グリッドから選択する最小の OS が、暗黙的な下限になります。  
* 許容される最小の OS の下限は、最初は、申請の最小の認定 OS レベル、つまり構成証明 OS レベルによって決まります。  自動的に決定されたこれらのレベルを下回る OS の下限を設定する必要がある場合は、OS の下限を設定する前にドライバーの拡張を実行する必要があります。

OS の下限は、ドライバーを配布できる最も古い Windows バージョンを示します。  この機能は、選択したオペレーティング システム以降でのみドライバーが提供されるように、暗黙的な下限を**上げる**場合に使用します。
最も一般的な使用事例については、「ドライバーの拡張」セクションの「[使用事例 2](#use-case-2--publishing-an-expanded-submission-to-a-specific-os-level)」をご覧ください。

### <a name="to-set-the-os-floor"></a>OS の下限を設定するには

1. 出荷ラベルを作成し、詳細を入力します。  詳細については、「[Windows Update にドライバーを公開する](publish-a-driver-to-windows-update.md)」を参照してください。
2. **[PNP を選択]** グリッド領域で、"*少なくとも 1 つ*" のハードウェア ID とオペレーティング システムの組み合わせを選択し、 **[公開]** をクリックします。
3. **[Restrict operating systems for driver distribution]\(ドライバー配布用のオペレーティング システムの制限)\** セクションまで下にスクロールし、 **[I want to restrict OS for driver distribution]\(ドライバーの配布用の OS を制限する\)** をオンにします。  この選択は、PNP グリッド内の少なくとも 1 つの項目に対して [公開] をクリックした "*後*" にのみ使用できるようになります。
4. **[Select Min OS Version (Floor)]\(最小 OS バージョン (下限) の選択\)** ドロップ ダウンから、ドライバーの配布先とする最も古い OS バージョンを選択します。

![OS バージョンを一覧表示するドロップダウン メニュー](images/restrict-floor.png)

PnP グリッドに表示されるオプションよりも前の OS の下限値を選択すると、次のエラーが表示されます。

![より新しい OS バージョンを選択するようユーザーに要求するエラー](images/restrict-floor-error-too-low.png)

## <a name="setting-an-os-ceiling"></a>OS の上限の設定

>[!NOTE]
> 上限機能へのアクセスは、有効なビジネス ニーズを持つ選択されたパートナー アカウントに限定されます。  質問がある場合は、[サポートにお問い合わせください](https://go.microsoft.com/fwlink/?linkid=2038065)。

上限は、ドライバーの配布先となる OS の上限を示します。 このオプションは、一覧表示されているオペレーティング システム リリース以下でドライバーを提供する場合に使用します。

たとえば、**RS3** (Windows 10、バージョン 1709) の上限値を選択した場合、ドライバーは RS4 (Windows 10、バージョン 1803) 以降を実行しているシステムには提供されません。

>[!IMPORTANT]
>OS の上限は、新しい OS に、ご自身のドライバーの基本的な機能に影響を与える破壊的変更があった場合にのみ設定する必要があります。 Microsoft では、OS の上限を要求するときに、ビジネス上の正当な理由を提出することを求めています。

### <a name="to-set-the-os-ceiling"></a>OS の上限を設定するには

1. 出荷ラベルを作成し、詳細を入力します。  詳細については、「[Windows Update にドライバーを公開する](publish-a-driver-to-windows-update.md)」を参照してください。
2. **[PNP を選択]** グリッド領域で、"*少なくとも 1 つ*" のハードウェア ID とオペレーティング システムの組み合わせを選択し、 **[公開]** をクリックします。
3. **[Restrict operating systems for driver distribution]\(ドライバー配布用のオペレーティング システムの制限)\** セクションまで下にスクロールし、 **[I want to restrict OS for driver distribution]\(ドライバーの配布用の OS を制限する\)** を選択します。  この選択は、PNP グリッド内の少なくとも 1 つの項目に対して [公開] をクリックした "*後*" にのみ使用できるようになります。
4. **[Select Max OS Version (Ceiling)]\(最大 OS バージョン (上限) の選択\)** ドロップ ダウンから、ドライバーの配布先とする最も古い OS バージョンを選択します。

![OS の上限を制限するための選択を示すダイアログ](images/restrict-ceiling.png)

>[!NOTE]
>PnP グリッド内から公開された最大の OS と同じかそれより低い OS 上限のみを選択できます。

選択が無効な場合は、ダッシュボードに次のエラーが表示されます。

![上限の選択が無効であることを示すエラー ダイアログ](images/restrict-ceiling-error.png)

## <a name="driver-expansion-expanding-a-drivers-lowest-os-target"></a>ドライバーの拡張:ドライバーの最小 OS ターゲットの拡張

ドライバーの配布を拡張する場合は、以下の重要情報に注意してください。

* 拡張を実行できるのは、**元の申請の所有者**だけです。 共有申請の受信者には、このオプションは表示されません。 (「[重要情報](#important-information)」を参照。)  
* 拡張は、申請ごとに一度だけ実行することができ、元に戻すことはできません。  既に実行された場合、[拡張] ボタンはグレー表示されます。
* 拡張は、[INF Manufacturer セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)で NTamd64.10.0...**14393** などの \[BuildNumber] *TargetOSVersion* 装飾が使用されていないドライバーに対してのみ実行されます。
* Windows 10 システムを対象として**上位**拡張できるのは Windows 8.1 ドライバーのみです。  Windows 10 のドライバーは、**下位**に拡張することができます。
* 拡張によって、ドライバーの認定のレベルに変更や追加は行われません。  ドライバーが RS5 に対して認定されている場合、拡張によって追加の下位 OS 認定が提供されることはありません。

ドライバーの拡張機能では、すべてのバージョンの Windows 10 を対象とする機能がパートナーに付与されます。  Windows 8.1 ドライバーを Windows 10 システムに提供することもできます。

これを行うには、申請パッケージ内で "*サポートされている*" INF ごとに、"*Windows 10 Client バージョン 1506 および 1511 (TH1)* " と *Windows Server 2016 x64 (TH1)* の新しい**拡張** PNP グリッド エントリを作成します。   これは、出荷ラベル内の共有ワークフローと公開ワークフローの両方に対して機能します。 次のスクリーン ショットは、Windows 8.1 ドライバーの拡張ボタンと Windows 10 ドライバーの拡張ボタンを示しています。

![Windows 8.1 ドライバーの拡張ボタン](images/expand-to-win10.png)

![Windows 10 ドライバーの拡張ボタン](images/expand-down-th1.png)

たとえば、次の申請は Windows 10 クライアント バージョン 1809 クライアント x64 (RS5) に対して認定されています。  拡張後、2 つの新しい **[拡張]** PNP グリッド エントリが作成されていることがわかります。

![申請に拡張グリッド エントリがあることを示す UI](images/expansion-pnpgrid-outline.png)

この申請に複数の INF が存在する場合、その中の各 INF とハードウェア ID は同じ新しい**拡張**エントリを受け取ります。  例外は、[INF Manufacturer](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section) セクションで *\[BuildNumber] TargetOSVersion* 装飾 (NTamd64.10.0...**14393** など) が使用されている場合です。  これらの INF はスキップされるため、拡張できません。  つまり、PNP グリッドに含まれるのは、部分的に拡張された一連の INF のみになります。  すべての INF ファイルを拡張する場合は、INF を編集し、*BuildNumber* を削除する必要があります。  また、サポートされる INF がない場合は、 **[拡張]** オプション ボックスが表示されないことがあります。

**拡張**エントリを作成したら、それを共有または公開できます。

ほとんどの場合、拡張されたドライバーを TH1 以降に提供する必要はありません。  代わりに、通常はその間のどこかで開始します。  そのため、出荷ラベルの作成の一環として、[OS の下限制限](#setting-an-os-floor)も忘れずに設定する必要があります。

次に、最も一般的な 2 つの使用事例と、それらを実現するための手順を示します。  上記のトースター申請を例として使用します。

## <a name="use-cases-for-limiting-or-expanding-driver-distribution-based-on-os"></a>OS に基づいてドライバーの配布を制限または拡張するための使用事例

トースターの例 (前のスクリーンショットを参照) を使用して、OS バージョンに基づいてドライバーの配布を設定する 2 つの一般的な使用シナリオについて説明します。

* **使用事例 1:拡張された申請を OEM と共有する IHV**  OEM は RS3 と RS4 のクライアントを対象にすることを希望していますが、申請は RS5 についてのみ認定を受けています。  OEM パートナーに対してこれを有効にして、独自の Windows Update 出荷ラベルを作成できるようにするにはどうすればよいですか?
* **使用事例 2:拡張された申請を特定の OS レベルに公開する**  RS5 認定ドライバーを Windows Update に公開して、RS3 以降を対象とすることを希望しています。  それを実現する方法を教えてください。

### <a name="use-case-1-an-ihv-sharing-an-expanded-submission-to-an-oem"></a>使用事例 1:拡張された申請を OEM と共有する IHV

申請の所有者だけが申請を拡張できます。

1. **[Expand to lower versions of Windows 10 (Starting from TH1)]\(下位バージョンの Windows 10 (TH1 以降) に拡張する\)** をクリックします。
2. OEM が必要とする各ハードウェア ID に対して **[共有]** を選択し、**Windows 10 クライアント バージョン 1506 および 1511 x64 (TH1)** の**拡張**エントリが含まれていることを確認します。  これは実際に、Windows Update によって将来に向かって提供するときに共有する必要がある唯一の OS エントリです (「[重要な情報](#important-information)」を参照)。

![ドライバーは共有されていないが OS が選択されていることを示すスクリーンショット](images/pending-share_example1.png)

3. ページの一番下までスクロールし、 **[公開]** をクリックして共有アクションを確定します。
4. OEM に、このページにアクセスし、「[使用事例 2](#use-case-2--publishing-an-expanded-submission-to-a-specific-os-level)」を読むように伝えます。  

既にドライバーをパートナーと共有している場合は、後で拡張し、追加の拡張された項目を共有することができます。  ただし、元の共有申請は非推奨とされ、パートナーは最新の共有申請のみ使用できるようになることに注意してください (非推奨の項目について詳しくは、「[[取り消し]/[すべて取り消し]](sharing-drivers-with-your-partners.md#revokerevoke-all)」セクションをご覧ください)。

### <a name="use-case-2--publishing-an-expanded-submission-to-a-specific-os-level"></a>使用事例 2:拡張された申請を特定の OS レベルに公開する

Windows 10 RS5 (1809) ドライバーを、PNP グリッドに記載されているものよりも低い OS (例: RS3) に公開することを希望しています。  まず、申請を**拡張**する必要があります。  この申請を IHV から受け取った場合、IHV では拡張タスクを完了してから、拡張した項目を共有する必要があります (「[使用事例 1](#use-case-1-an-ihv-sharing-an-expanded-submission-to-an-oem)」を参照)。  

ドライバーの拡張が完了した後、申請パッケージ内でサポートされている INF ごとに、"*Windows 10 クライアント バージョン 1506 および 1511 (TH1)* " と *Windows Server 2016 x64 (TH1)* の新しい**拡張** PNP グリッド エントリが作成されます。  これは、公開する必要があるこれらの項目のいずれかになります。
上記の拡張されたトースターの例を使用すると、これは RS3 が下限になるように公開するための正しい方法です。

1. *hid\toaster&col02* と "*Windows 10 クライアント バージョン 1506 および 1511 x64 (TH1) **" 項目に対して** [公開]* を選択します。 これにより、暗黙的な下限が **TH1** に設定されます。

![スクリーンショットには、バージョンが選択され、状態が [Not on Windows Update]\(Windows Update 上にない\) に設定された申請が示されています](images/expansion-pnpgrid-example1.png)

2. 出荷ラベルでは、このように [状態] 列に [Pending publishing]\(公開保留中\) と表示されます。

![スクリーンショットには、バージョンが選択され、状態が [Pending publishing]\(公開保留中\) に設定された申請が示されています](images/expansion-pnpgrid-pending-example1.png)

3. **[Restrict operating systems for driver distribution]\(ドライバー配布用のオペレーティング システムの制限)\** セクションまで下にスクロールし、 **[I want to restrict OS for driver distribution]\(ドライバーの配布用の OS を制限する\)** を選択します。
4. **[Select Min OS Version (Floor) for this driver]\(このドライバーの最小 OS バージョン (下限) の選択\)** ドロップダウンから、 **[RS3]** を選択します。

![最小 OS バージョン (下限) を選択する UI](images/restrict-floor-example1.png)

5. ページの一番下までスクロールし、 **[公開]** をクリックして公開要求を確定します。

このドライバーが公開され、RS3 以降のすべての OS バージョンに適用されます。

## <a name="faq"></a>FAQ

### <a name="why-cant-i-check-the-restrict-operating-systems-for-driver-distribution-box"></a>[Restrict operating systems for driver distribution]\(ドライバー配布用のオペレーティング システムの制限)\ ボックスをオンにできないのはなぜですか?

**[PNP を選択]** セクションで、最初に少なくとも 1 つのハードウェア ID エントリに対して **[公開]** をクリックしたことを確認します。

### <a name="the-expand-to-lower-versions-of-windows-10-starting-from-th1-box-is-greyed-out-or-missing"></a>[Expand to lower versions of Windows 10 (Starting from TH1)]\(下位バージョンの Windows 10 (TH1 以降) に拡張する\) ボックスがグレー表示されているか、見つかりません

ボックスがグレー表示されている場合は、申請が既に拡張されていることを意味します。

ボックスがない場合は、2 つのうちいずれかを意味します。  ご自身が初期申請の所有者でないか、または INF に BuildNumber セクションが含まれています。  「[重要情報](#important-information)」をご覧ください。

### <a name="how-can-i-target-a-windows-version-that-is-older-than-my-drivers-certification"></a>ドライバーの認定よりも古い Windows バージョンをターゲットにするにはどうすればよいですか?

「[使用事例 2](#use-case-2--publishing-an-expanded-submission-to-a-specific-os-level)」をご覧ください。

### <a name="some-of-my-infs-are-missing-after-expansion--why-cant-i-expand-my-entire-submission"></a>拡張後に一部の INF がありません。  申請全体を拡張できないのはなぜですか?

申請内の各 INF は、拡張について個別に評価されます。 一部またはすべての INF ([INF Manufacturer](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section) に関する記事を参照) で *\[BuildNumber] TargetOSVersion* 装飾が使用されている場合、その INF を拡張する処理は失敗します。 申請を拡張する必要がある場合は、まず INF を編集して \[BuildNumber] を削除する必要があります。 \[BuildNumber] が含まれない INF は正常に処理されます。  詳しくは、「[重要な情報](#important-information)」をご覧ください。
