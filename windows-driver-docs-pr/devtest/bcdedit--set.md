---
title: BCDEdit/set
description: BCDEdit]、[set コマンドは、Windows ブート構成データ ストア (BCD) の Windows 7、Windows Server 2008、Windows 8、Windows 8.1、Windows 10、Windows Server 2012、および Windows Server 2012 R2 のブート エントリ オプション値を設定します。
ms.assetid: e66d9c55-9a44-4de2-a1a4-634c7d550735
ms.date: 07/09/2018
keywords:
- BCDEdit/set ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /set
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1928c242ddde8f7fa0184fa95d2712220fa79186
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549079"
---
# <a name="bcdedit-set"></a>BCDEdit/set

**BCDEdit/set**コマンドは、Windows ブート構成データ ストア (BCD) の Windows 7、Windows Server 2008、Windows 8、Windows 8.1、Windows 10、Windows Server 2012、および Windows Server 2012 R2 のブート エントリ オプション値を設定します。 使用して、 **BCDEdit/set**カーネル デバッガーの設定、メモリのオプション、またはテスト署名されたカーネル モード コードまたは負荷代替ハードウェア アブストラクション レイヤー (HAL) を有効にするオプションなどの特定のブート エントリの要素を構成するコマンドとカーネル ファイル。 ブート エントリのオプションを削除するには、使用、 [ **BCDEdit/deletevalue** ](bcdedit--deletevalue.md)コマンド。

> [!CAUTION]
> BCDEdit を使用して BCD を変更するには、管理者特権が必要です。 使用してオプションのいくつかのブート エントリを変更、 **BCDEdit/set**コマンドしなくなる可能性コンピューター。 代わりに、システム構成ユーティリティ (MSConfig.exe) を使用して、ブート設定を変更します。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

```syntax
bcdedit  /set [{ID}] datatype value
```

## <a name="parameters"></a>パラメーター

\[**{ID}**\]  
**{ID}** ブート エントリに関連付けられた GUID です。 指定しない場合、 **{ID}** のコマンドは、現在のオペレーティング システムのブート エントリを変更します。 ブート エントリに関連付けられた GUID を中かっこで囲む必要がありますブート エントリが指定されている場合 **{}** します。 すべてのアクティブなブート エントリの GUID 識別子を表示する、 **bcdedit/enum**コマンド。 現在のブート エントリの識別子は **{現在}** します。 このオプションの詳細については、次のコマンドを使用: **bcdedit/でしょうか。ID**

> [!NOTE]
> 使用する場合[Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=108518)、たとえばブート エントリの識別子を囲む引用符を使用する必要があります: **"{49916baf-0e08-11db-9af4-000bdbd316a0}"** または **"{current}"**.

*datatype* *value*  

以下に示すいくつかの便利な*datatypes*と関連付けられた*値*します。

**bootlog** \[ **yes** | **no** \]  
システムの初期化ログを有効にします。 このログは、%WINDIR% ディレクトリで Ntbtlog.txt ファイルに格納されます。 テキスト形式で読み込まれ、アンロードされたドライバーの一覧が含まれています。

**bootmenupolicy** \[ **レガシ** | **標準** \]  
システムは、使用するブート メニューの種類を定義します。 既定では ForWindows 10、Windows 8.1、Windows 8 および Windows RT**標準**します。 Windows Server 2012 R2、Windows Server 2012 では、既定値は**レガシ**します。 ときに**レガシ**が選択されている、高度なオプション メニュー (**F8**) は使用できます。 ときに**標準**が選択されている特定の状況でのみ、ブート メニューが表示されます: たとえば、起動している場合の修復のディスクまたはインストール メディアから複数のブート エントリを構成している場合、起動時に障害がある場合、、または高度なスタートアップを使用するコンピューターを手動で構成した場合。 ときに**標準**が選択されている、 **F8**キーは、ブート時に無視されます。 Windows 8 Pc すばやく起動キーを押してに十分な時間がないように**F8**します。 詳細については、[(セーフ モードなど)、Windows スタートアップ設定](https://go.microsoft.com/fwlink/p/?linkid=313921)を参照してください。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降から使用できます。 使用することも、 **onetimeadvancedoptions**高度なオプションを使用する (**F8**) メニュー (**レガシ**) 次のブート時に 1 回です。

**bootstatuspolicy** *policy*

ブートの状態のポリシーを制御します。 ブート状態*ポリシー*次のいずれかを指定できます。

- `DisplayAllFailures`:失敗したブート、失敗したシャット ダウン、または失敗したチェックポイントがある場合は、すべてのエラーが表示されます。 コンピューターの再起動時に Windows 回復環境にフェールオーバーされます。

- `IgnoreAllFailures`:失敗したブート、失敗したシャット ダウン、または失敗したチェックポイントがある場合は、エラーを無視します。 コンピューターは、エラーの発生後に通常どおりにブートしようとします。

- `IgnoreShutdownFailures`:のみ障害が発生したシャット ダウンがある場合は、エラーを無視します。 失敗したシャット ダウンされた場合は、コンピューターに自動的にフェールオーバーしないの再起動時に Windows 回復環境にします。 これは、Windows 8 の既定の設定です。

- `IgnoreBootFailures`:だけ、失敗したブートがある場合は、エラーを無視します。 失敗したブートがある場合、コンピューターに自動的にフェールオーバーしないの再起動時に Windows 回復環境にします。

- `IgnoreCheckpointFailures`:のみ障害が発生したチェックポイントがある場合は、エラーを無視します。 失敗したチェックポイントがある場合、コンピューターに自動的にフェールオーバーしないの再起動時に Windows 回復環境にします。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

- `DisplayShutdownFailures`:失敗したシャット ダウンがある場合は、エラーを表示します。 失敗したシャット ダウンがある場合、コンピューターは経由での再起動時に Windows 回復環境では失敗します。 起動エラー、および失敗したチェックポイントを無視します。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

- `DisplayBootFailures`:失敗したブートがある場合は、エラーを表示します。 失敗したブートがある場合、コンピューターは経由での再起動時に Windows 回復環境では失敗します。 シャット ダウン エラーや障害が発生したチェックポイントを無視します。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

- `DisplayCheckpointFailures`:失敗したチェックポイントがある場合は、エラーを表示します。 失敗したチェックポイントがある場合、コンピューターは経由での再起動時に Windows 回復環境では失敗します。 起動とシャット ダウンの障害を無視します。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

**bootux** \[ **disabled** | **basic** | **standard** \]  
起動画面のアニメーションを制御します。 使用可能な値は、無効になっている、basic、および標準です。

> [!NOTE]
> Windows 8 および Windows Server 2012 でサポートされていません。

**disabledynamictick** \[ **はい** | **なし** \]  
有効にし、動的タイマーのティックの機能を無効にします。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

> [!NOTE]
> このオプションは、デバッグにのみ使用する必要があります。

**disableelamdrivers** \[ **はい** | **なし** \]  
早期起動マルウェア対策 (ELAM) ドライバーの読み込みを制御します。 OS ローダーは、セキュリティ上の理由には、このエントリを削除します。 このオプションは、F8 メニューを使用してのみトリガーされます。 このオプションをトリガーする (コンピューター) に物理的にユーザーがする必要があります。

> [!NOTE]
> このオプションは、デバッグにのみ使用する必要があります。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

**forcelegacyplatform** \[ **yes** | **no** \]  
強制的に従来の PC デバイスの存在を想定する OS などの点で CMO やキーボード コント ローラー。

> [!NOTE]
> このオプションは、デバッグにのみ使用する必要があります。 オプションは、Windows 8 および Windows Server 2012 以降から使用できます。

**サイズ** *maxsize* 、1 つのプロセッサ グループ内の論理プロセッサの最大数を設定、 *maxsize*は 1 ~ 64 の範囲での 2 の累乗します。 既定では、プロセッサ グループは、64 の論理プロセッサの最大サイズをあります。 このブート構成をテスト目的で、コンピューターのプロセッサ グループの構成とサイズをオーバーライドする設定を使用することができます。 [プロセッサ グループ](https://go.microsoft.com/fwlink/p/?linkid=155063)を 64 論理プロセッサを超えるコンピューターのサポートを提供します。 このブート オプションは、Windows 7 および Windows Server 2008 R2 の 64 ビット バージョンおよびそれ以降のバージョンで使用可能です。 このブート オプションには、Windows 7 の 32 ビット バージョンへの影響はありません。

使用して、**サイズ**場合、複数のグループを強制して、コンピューターに 64 個以下のアクティブな論理プロセッサ オプションを選択します。 詳細については、このオプションを使用して、[テスト ドライバは、複数のプロセッサ グループのサポートのブート パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff542298)を参照してください。

**groupaware** \[ **on** | **off** \]  
強制的にドライバーを使用して、複数のプロセッサ グループ環境で複数のグループに注意してください。 このオプションを使用して、ドライバーおよびコンポーネントでのグループ間の非互換性を公開します。 [プロセッサ グループ](https://go.microsoft.com/fwlink/p/?linkid=155063)を 64 論理プロセッサを超えるコンピューターのサポートを提供します。 このブート オプションは、Windows 7 および Windows Server 2008 R2 の 64 ビット バージョンおよびそれ以降のバージョンで使用可能です。 このブート オプションには、Windows 7 の 32 ビット バージョンへの影響はありません。 使用することができます、 **groupaware**オプションと**サイズ**コンピューターで 64 個以下のアクティブな論理プロセッサが関数に複数のグループのドライバーの互換性をテストするオプション。

**で groupaware**設定グループ 0 以外のプロセスが開始されているようになります。 これにより、ドライバーとコンポーネント間のグループ間の相互作用の機会が増えます。 オプションでは、従来の関数の動作も変更されます**KeSetTargetProcessorDpc**、 **KeSetSystemAffinityThreadEx**、および**KeRevertToUserAffinityThreadEx**、常にアクティブな論理プロセッサを含む最上位の番号付きグループで動作できるようにします。 呼び出すグループ対応、対応する従来これらの関数のいずれかを呼び出すドライバーを変更する必要があります (**KeSetTargetProcessorDpcEx**、 **KeSetSystemGroupAffinityThread**、および**KeRevertToUserGroupAffinityThread**)。

詳細については、このオプションを使用して、[テスト ドライバは、複数のプロセッサ グループのサポートのブート パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff542298)を参照してください。

**hal** *ファイル*オペレーティング システム ローダーで代替 HAL ファイルを読み込むように指示します。 指定したファイルは %systemroot% になければなりません\\system32 ディレクトリ。

**hypervisorbusparams** *Bus.Device.Function*  
PCI バス、デバイス、およびデバッグのデバイス数の関数を定義します。 たとえば、1.5.0 では、bus 1、5、関数 0 のデバイスでデバッグ デバイスをについて説明します。 デバッグするために、1394 ケーブルまたは USB 2.0 または 3.0 の USB デバッグ ケーブルを使用している場合は、このオプションを使用します。

**hypervisordebug** \[ **で** | **オフ** \]  
ハイパーバイザーのデバッガーが有効になっているかどうかを制御します。

**シリアル**  
デバッグ用のシリアル接続を指定します。 ときに、**シリアル**オプションを指定すると、設定することも、 **hypervisordebugport**と**hypervisorbaudrate**オプション。

``` syntax
bcdedit /set hypervisordebugtype serial
bcdedit /set hypervisordebugport 1
bcdedit /set hypervisorbaudrate 115200
bcdedit /set hypervisordebug on
bcdedit /set hypervisorlaunchtype auto
```

**1394**  
デバッグの IEEE 1394 (FireWire) 接続を指定します。 このオプションを使用する場合、 **hypervisorchannel**オプションも設定する必要があります。

**Net**  
デバッグするためのイーサネット ネットワーク接続を指定します。 このオプションを使用する場合、 **hypervisorhostip**オプションが設定されていないこともあります。

**hypervisorhostip** *IP アドレス*(使用される場合にのみ、 **hypervisordebugtype**は**Net**)。ハイパーバイザーをデバッグするには、ネットワーク接続経由で、ホストのデバッガーの IPv4 アドレスを指定します。 HYPER-V でのデバッグ方法の詳細については、[、Hyper-v と仮想マシンを作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)を参照してください。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisorhostport** \[ *port* \]  
(使用される場合にのみ、 **hypervisordebugtype**は**Net**)。ネットワークのデバッグにも、ホストのデバッガーとの通信にポートを指定します。 49152 またはそれ以降にする必要があります。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisordhcp** \[ **yes** | **no** \]  
ハイパーバイザーで使用するネットワーク デバッガーでは、DHCP の使用を制御します。 これを設定**ありません**の自動プライベート IP アドレス指定 (APIPA) のローカル リンクの IP アドレスを取得する使用を強制します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisoriommupolicy** \[ **既定** | **を有効にする** | **を無効にします。**\]  
ハイパーバイザーが、入力出力メモリ管理ユニット (IOMMU) を使用するかどうかを制御します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisorlaunchtype** \[ **オフ** | **自動** \]  
ハイパーバイザーの起動オプションを制御します。 ターゲット コンピューターで HYPER-V をデバッグするデバッガーを設定する場合は、このオプションを設定**自動**ターゲット コンピューターにします。 詳細については、[、Hyper-v と仮想マシンを作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)を参照してください。

**hypervisorloadoptions NOFORCESNOOP** \[ **はい** | **なし** \]  
ハイパーバイザーがシステム IOMMUs snoop 制御を適用する必要があるかどうかを指定します。

**hypervisornumproc** *number*  
ハイパーバイザーで開始できる論理プロセッサの合計数を指定します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisorrootproc** *number*  
ルート パーティション内の仮想プロセッサの最大数を指定して、開始はハイパーバイザー内での論理プロセッサを持つことができる分割後の Non-uniform Memory アーキテクチャ (NUMA) ノードの数を制限します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisorrootprocpernode** *number*  
ルート パーティションに事前に分割、Non-uniform Memory アーキテクチャ (NUMA) ノード内で開始できる仮想プロセッサの合計数を指定します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisorusekey** \[ *キー* \]  
(使用される場合にのみ、 **hypervisordebugtype**は**Net**)。ネットワークのデバッグにも、接続の暗号化に使用するキーを指定します。 \[0 ~ 9\]と\[a ~ z\]のみ許可します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**hypervisoruselargevtlb** \[ **はい** | **ありません**変換ルック アサイド バッファー (TLB) の仮想領域サイズが増加します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**increaseuserva** *メガバイト*ユーザー モード仮想アドレス領域のメガバイト単位でメモリの量を指定します。

Windows の 32 ビット エディションで 4 ギガバイト (GB) の使用可能な仮想アドレス領域があるアプリケーション。 2 GB は、アプリケーションで使用できると、その他の 2 GB はシステムでのみ使用できるように、仮想アドレス空間が分割されます。

有効になっている、4 ギガバイトのチューニング機能、 **increaseuserva**オプションを使用すると、アプリケーションに提供される仮想アドレス領域を増やす 3 GB まで、1 と 2 の間にシステムで利用できる量を減らしますGB。 **BCEdit/set increaseuserva** *メガバイト*コマンドは、2048 (2 GB) から 3072 (3 GB) までの値を指定できますメガバイト単位の 10 進表記でします。 Windows では、カーネル モード アドレス空間として残りのアドレス空間 (指定された量の 4 GB) を使用します。

参照してください[4 ギガバイトのチューニング (Windows)](https://docs.microsoft.com/windows/desktop/Memory/4-gigabyte-tuning)詳細については、この機能はします。

**カーネル***ファイル*オペレーティング システム ローダーで代替のカーネルを読み込むように指示します。 指定したファイルは %systemroot% になければなりません\\system32 ディレクトリ。

**loadoptions busparams**=*Bus.Device.Function*複数のコント ローラーが存在する場合は、ターゲット コント ローラーを指定します。 この構文は、デバッグを 1394 ケーブルまたは USB 2.0 デバッグ ケーブルを使用する場合に適しています。 *バス*バス番号を指定します*デバイス*デバイス番号を指定し、*関数*関数の数を指定します。

> [!NOTE]
> 1394 デバッグ、バス パラメーターを構成している Windows のバージョンに関係なく、10 進数で指定する必要があります。 USB 2.0 のデバッグに使用されるバス パラメーターの形式は、Windows のバージョンによって異なります。 Windows Server 2008 では、16 進数で、USB 2.0 bus パラメーターを指定してください。 Windows 7 および Windows Server 2008 R2 以降のバージョンの Windows では、10 進数で、USB 2.0 バスのパラメーターを指定する必要があります。

**maxgroup** \[ **on** | **off** \]  
プロセッサ グループの構成で作成されたグループの数を最大化します。

**で maxgroup**設定では、特定のコンピューターのグループの数を最大化する方法でグループに NUMA ノードが割り当てられます。 作成されたグループの数がコンピューターが NUMA ノードの数またはこのバージョンの Windows でサポートされているグループの最大数、小さい方です。 既定の動作 (**オフ maxgroup)** としていくつかのグループに限り、NUMA ノードを緊密にパックされます。

複数のグループを使用する、コンピューターが 64 個以下のアクティブな論理プロセッサと、コンピューターに複数の NUMA ノードが既にある場合は、このオプションを使用します。 このオプションは、64 を超える論理プロセッサを搭載したコンピューターの既定のグループの構成を変更することも使用できます。

[プロセッサ グループ](https://docs.microsoft.com/windows/desktop/ProcThread/processor-groups)を 64 論理プロセッサを超えるコンピューターのサポートを提供します。 このオプションは、Windows 7 および Windows Server 2008 R2 の 64 ビット バージョンおよびそれ以降のバージョンで利用できます。 このブート オプションには、Windows 7 の 32 ビット バージョンへの影響はありません。

詳細については、このオプションを使用して、[テスト ドライバは、複数のプロセッサ グループのサポートのブート パラメーター](boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)を参照してください。

**nointegritychecks** \[ **で** | **オフ**\]整合性チェックを無効にします。 セキュア ブートが有効な場合は設定できません。 この値は、Windows 7 と Windows 8 によって無視されます。

**nolowmem** \[ **で** | **オフ**\]メモリ不足の使用を制御します。 ときに**で nolowmem**が指定されて、このオプションはオペレーティング システム、デバイス ドライバー、およびすべてのアプリケーションを 4 GB の境界より上のアドレスにロードし、4 GB の境界上にあるすべてのメモリ プールの割り当てを Windows に指示します。 なお、 **nolowmem** Windows 8、Windows Server 2012、および以降のバージョンの Windows のオプションは無視されます。

**novesa** \[ **で** | **オフ** \] VGA ドライバーが VESA BIOS の呼び出しを避ける必要があるかどうかを示します。 Windows 8 および Windows Server 2012 では、オプションは無視されます。

**novga** \[ **で** | **オフ** \] OS の VGA モードの使用を無効にします。 オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**nx** \[**Optin |OptOut | AlwaysOn |AlwaysOff**\]  
有効にし、無効化、データ実行防止 (DEP)、一連のハードウェアとソフトウェアのテクノロジを有害なコードが保護されたメモリの場所で実行されていることを防ぐために設計されていますを構成します。 DEP 設定については、[データ実行防止](https://docs.microsoft.com/windows/desktop/Memory/data-execution-prevention)を参照してください。

**Optin**  
DEP は、Windows カーネルやドライバーなど、オペレーティング システムのコンポーネントに対してのみ使用できます。 管理者は、Application Compatibility Toolkit (ACT) を使用して、選択した実行可能ファイルで DEP を有効にできます。

**Optout**  
オペレーティング システムと Windows カーネルやドライバーなど、すべてのプロセスの DEP を使用できます。 管理者が選択されている実行可能ファイルに DEP を無効を使用して、**システム**で**コントロール パネルの **します。

**AlwaysOn**  
オペレーティング システムと Windows カーネルやドライバーなど、すべてのプロセスの DEP を使用できます。 DEP を無効にする試行をすべてが無視されます。

**AlwaysOff**  
DEP. を無効にします。 選択的に DEP を有効にしようとは無視されます。

Windows vista では、このパラメーターには、物理アドレス拡張 (PAE) も無効にします。 このパラメーターは、Windows Server 2008 で、PAE を無効にできません。

**onecpu** \[ **on** | **off** \]  
ブートの 1 つ以上の論理プロセッサを搭載したコンピューターで使用される CPU のみを強制します。

たとえば、次のコマンドは、1 つのプロセッサを使用して、現在のオペレーティング システム ローダーを構成します。

```syntax
bcdedit /set onecpu on
```

**onetimeadvancedoptions** \[ **on** | **off** \]  
次の起動時には、従来のメニュー (F8 メニュー) に、システムで起動したかどうかを制御します。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

```syntax
bcdedit /set {current} onetimeadvancedoptions on
```

**pae** \[ **既定** | **ForceEnable** | **ForceDisable** \]  
有効または、物理アドレス拡張 (PAE) を無効にします。 PAE を有効にすると、システムは、PAE カーネルのバージョン、Windows を読み込みます。

**Pae**パラメーターは、x86 ベースおよび x64 ベース プロセッサを搭載したコンピューターで実行される Windows の 32 ビット バージョンのブート エントリでのみ有効です。 (Windows 8) より前の Windows の 32 ビット バージョンでは、PAE は既定で無効になります。 ただし、Windows に自動的にコンピューターが構成されている場合、PAE を有効にホット アド メモリ デバイス 4 GB の領域を超えるメモリ範囲で静的リソース アフィニティ テーブル (SRAT) で定義されています。 *ホット アド メモリ*メモリ デバイスの再起動またはコンピューターをオフにすることがなく追加することができますをサポートします。 ここでは、システムの起動時に、PAE を有効にする必要があります、ため、それを有効に自動的にように、システムは、再起動の間で追加される拡張のメモリに迅速に対応できます。 ホット アド メモリが、Datacenter Edition、Windows Server 2008 でのみサポートされます。Windows Server 2008 for Itanium-based Systems;上のすべての以降のバージョンの Windows Server datacenter および enterprise エディションとします。 さらに、Windows Server 2008 より前の Windows のバージョンは、ホット アド メモリが、ACPI BIOS、x86 コンピューターでのみサポートされているプロセッサ、および特殊なハードウェア。 Windows Server 2008 と Windows Server の以降のバージョンでは、すべてのプロセッサ アーキテクチャのことができます。

ハードウェアが有効なデータ実行防止 (DEP) をサポートし、DEP をサポートする Windows オペレーティング システムの 32 ビット バージョンを実行しているコンピューターで PAE は自動的にで有効に DEP が有効にすると、動作する Windows のすべての 32 ビット バージョンDEP. を無効にすると、Windows Server 2003 SP1、PAE を除く、システムが無効になっています DEP を無効にするには、PAE を有効にする、する必要があります有効にする PAE、明示的を使用して **/set nx AlwaysOff**と **/set pae ForceEnable**します。 DEP の詳細については、[DEP の構成と PAE のブート パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff542275)を参照してください。

使用しての詳細については、 **pae**パラメーターと PAE の構成に影響する他のパラメーターを参照してください。 [DEP の構成と PAE のブート パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff542275)します。

**pciexpress** \[ **default** | **forcedisable**\]  
有効または、PCI Express 機能を無効にします。 コンピューターのプラットフォームが、PCI Express 機能と、ACPI をサポートしているか\_OSC メソッドは、Windows により、高度な機能で (これは、既定値)、PCI Express のネイティブ コントロール機能という、オペレーティング システムへの機能の制御を許可します。 使用して、 **forcedisable**高度な PCI Express 機能を変更し、PCI Express の従来の動作を使用するオプション。 詳細については、[を有効にする PCI Express 内のネイティブ コントロール Windows](https://msdn.microsoft.com/library/windows/hardware/gg487424.aspx)を参照してください。

**quietboot** \[ **on** | **off** \]  
Windows 起動画面の表示とアニメーションの代わりに高解像度ビットマップの表示を制御します。 Windows Vista では、以前のオペレーティング システムで、**選択する**と同様の機能を提供します。

> [!NOTE]
> 使用しないでください、 **quietboot** Windows 8 のオプションだけでなくすべてのブート グラフィックスのバグ チェックのデータの表示ができなくなります。

**removememory** *メガバイト*からオペレーティング システムが使用できる使用可能なメモリの合計メモリを削除します。

たとえば、次のコマンドは、指定されたブート エントリに関連付けられたオペレーティング システムに使用可能な総から 256 MB のメモリを削除します。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} removememory 256
```

**sos** \[ **on** | **off** \]  
ブート プロセス中に、読み込み時に、ドライバーの名前の表示を制御します。 使用**で sos**名を表示します。 使用**オフ sos**を表示しないようにします。

**testsigning** \[ **on** | **off** \]  
Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008、または Windows Vista があらゆる種類のテスト署名されたカーネル モード コードを読み込むかどうかを制御します。 64 ビット バージョンの Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 では、どの意味テスト署名されたカーネル モード ドライバーに、このオプションはない、既定で設定して、Windows Vista は、既定では読み込まれません。 BCDEdit のコマンドを実行した後は、変更を反映できるようにコンピューターを再起動します。 詳細については、[テスト署名の概要](https://msdn.microsoft.com/library/windows/hardware/ff547660)を参照してください。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

**tpmbootentropy** \[ **既定** | **ForceEnable** | **ForceDisable**\]  
エントロピがトラステッド プラットフォーム モジュール (TPM) ため、オペレーティング システムの乱数ジェネレーターのシードから収集されたかどうかを判断します。

**truncatememory** *アドレス*Windows で使用できる物理メモリの量を制限します。 このオプションを使用する場合、Windows は、指定された物理アドレス以上のすべてのメモリを無視します。 指定、*アドレス*(バイト単位)。

たとえば、次のコマンドは、1 GB で、物理アドレスの制限を設定します。 (1073741824) を 10 進数または 16 進数 (0x40000000) アドレスを指定することができます。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} truncatememory 0x40000000
```

**tscsyncpolicy** \[ **既定** | **レガシ** | **拡張** \]  
コントロール、時刻、タイムスタンプ カウンター同期ポリシー。 このオプションは、デバッグにのみ使用する必要があります。

> [!NOTE]
> オプションは、Windows 8 および Windows Server 2012 以降を使用します。

**usefirmwarepcisettings** \[ **yes** | **no** \]  
有効または、BIOS 構成されている周辺機器コンポーネント相互接続 (PCI) リソースの使用を無効にします。

**useplatformclock** \[ **yes** | **no** \]  
システムのパフォーマンス カウンターとしてのプラットフォームのクロックの使用を強制します。

> [!NOTE]
> このオプションは、デバッグにのみ使用する必要があります。

**uselegacyapicmode** \[ **yes** | **no** \]  
拡張 APIC モードをサポートしているプロセッサ、チップセット場合でも、以前のバージョンの APIC モードを強制的に使用します。

**useplatformtick** \[ **はい** | **なし** \]  
合成のタイマーは許可されていません、プラットフォーム ソースでバックアップするクロックを強制します。 オプションは、Windows 8 および Windows Server 2012 以降を使用します。

> [!NOTE]
> このオプションは、デバッグにのみ使用する必要があります。

**vga** \[ **on** | **off** \]  
安全な解像度の使用を強制します。 たとえばを Windows 7 を実行するコンピューターこのオプションは 640 x 480 の解像度の使用を強制します。 Windows 8 を実行するコンピューターでは、このオプションは、800 x 600 の解像度がある場合または 640 x 480 の使用をしない強制します。

**xsavedisable** \[ **0** | **1** \]  
ときにゼロ (0) 以外の値に設定するには、カーネルで XSAVE プロセッサ機能が無効にします。

**x2apicpolicy** \[ **enable** | **disable** \]  
有効またはサポートされている場合は、拡張の APIC モードの使用を無効にします。 使用するシステムの既定値は拡張可能な場合の APIC モードです。

### <a name="comments"></a>コメント

BCD の特定の要素とブート オプションの詳細については、コマンドを使用することができます**BCDEdit/でしょうか。OSLOADER**と**BCDEdit/でしょうか。型の OSLOADER**します。

現在のブート エントリとその設定を表示する、 **bcdedit/enum**コマンド。 このコマンドは、アクティブなブート エントリは、関連付けられているグローバル一意識別子 (GUID) を表示できます。 識別子を使用して、 **/set**コマンドは、特定のブート エントリのオプションを構成します。

設定したブート オプションの値を削除するには、使用、 **/deletevalue**オプション。 コマンドの構文は次のとおりです。

**bcdedit** /**deletevalue** \[**{ID}**\] *datatatype*

たとえば、プロセッサ グループ オプションを変更する**サイズ**をテスト用の新しい値を目的として、次のコマンドを入力し、コンピューターを再起動して、64 の既定値に戻すことができます。

``` syntax
bcdedit /deletevalue groupsize
```

ブート オプションの変更には、再起動を有効にする必要があります。 一般的に使用される BCDEdit のコマンドについては、[ブート構成データ エディターに関してよく寄せられる質問](https://go.microsoft.com/fwlink/p/?linkid=155086)を参照してください。

## <a name="requirements"></a>要件

|||
|----|----|
|サポートされている最小のクライアント|Windows Vista|
|サポートされている最小のサーバー|Windows Server 2008|
|||

## <a name="see-also"></a>関連項目

- [BCDEdit/deletevalue](bcdedit--deletevalue.md)
