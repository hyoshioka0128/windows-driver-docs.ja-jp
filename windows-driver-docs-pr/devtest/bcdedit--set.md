---
title: BCDEdit /set
description: BCDEdit /set コマンドでは、Windows 7、Windows Server 2008、Windows 8、Windows 8.1、Windows 10、Windows Server 2012、Windows Server 2012 R2 の Windows ブート構成データ ストア (BCD) のブート エントリ オプション値を設定します。
ms.assetid: e66d9c55-9a44-4de2-a1a4-634c7d550735
ms.date: 02/07/2018
keywords:
- BCDEdit /set ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /set
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: 088372dd352e0fd6fb3fa2dff629f9d84845036b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967981"
---
# <a name="bcdedit-set"></a>BCDEdit /set

**BCDEdit /set** コマンドでは、Windows ブート構成データ ストア (BCD) のブート エントリ オプション値を設定します。 **BCDEdit /set** コマンドは、カーネル デバッガーの設定、メモリ オプション、テスト署名されたカーネル モード コードを有効にするオプション、代替ハードウェア アブストラクション レイヤー (HAL) やカーネル ファイルを読み込むオプションなど、特定のブート エントリ要素を構成するために使用します。 ブート エントリ オプションを削除するには、[**BCDEdit /deletevalue**](bcdedit--deletevalue.md) コマンドを使用します。

> [!CAUTION]
> BCD を変更するために BCDEdit を使用するには、管理者特権が必要です。 **BCDEdit /set** コマンドを使用して一部のブート エントリ オプションを変更すると、コンピューターが動作しなくなる可能性があります。 別の方法として、システム構成ユーティリティ (MSConfig.exe) を使用してブート設定を変更します。

> [!NOTE]
> BCDEdit のオプションを設定する前に、コンピューターで BitLocker とセキュア ブートを無効にするか中断することが必要になる場合があります。

```syntax
bcdedit  /set [{ID}] datatype value
```

## <a name="parameters"></a>パラメーター

\[ **{ID}** \]  
**{ID}** は、ブート エントリに関連付けられている GUID です。 **{ID}** を指定しなかった場合、このコマンドで現在のオペレーティング システムのブート エントリが変更されます。 ブート エントリを指定する場合は、ブート エントリに関連付けられている GUID を中かっこ **{ }** で囲む必要があります。 すべてのアクティブ ブート エントリの GUID 識別子を表示するには、**bcdedit /enum** コマンドを使用します。 現在のブート エントリの識別子は **{current}** です。 このオプションの詳細を表示するには、次のコマンドを使用します。**bcdedit /? ID**

> [!NOTE]
> [Windows PowerShell](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/?view=powershell-6) を使用している場合は、ブート エントリ識別子を引用符で囲む必要があります。たとえば、 **"{49916baf-0e08-11db-9af4-000bdbd316a0}"** または **"{current}"** です。

*datatype* *value*  

次の一覧に、いくつかの便利な *datatype* とそれに関連付けられた *value* を示します。

**bootlog** \[ **yes** | **no** \]  
システム初期化ログを有効にします。 このログは、%WINDIR% ディレクトリの Ntbtlog.txt ファイルに記録されます。 読み込まれたドライバーとアンロードされたドライバーの一覧がテキスト形式で示されます。

**bootmenupolicy** \[ **Legacy** | **Standard** \]  
システムによって使用されるブート メニューの種類を定義します。 Windows 10、Windows 8.1、Windows 8、Windows RT の既定値は **Standard** です。 Windows Server 2012 R2、Windows Server 2012 の場合、既定値は **Legacy** です。 **Legacy** を選択した場合、[詳細オプション] メニュー (**F8** キー) を使用できます。 **Standard** を選択すると、ブート メニューは表示されますが、特定の状況に限られます。たとえば、起動時にエラーが発生した場合、修復ディスクまたはインストール メディアから起動している場合、複数のブート エントリを構成した場合、またはカスタマイズした起動を使用するようにコンピューターを手動で構成した場合などがあります。 **Standard** を選択した場合、ブート中に **F8** キーは無視されます。 Windows 8 PC は高速に起動するので、**F8** キーを押す十分な時間がありません。 詳細については、「[Windows のスタートアップ設定 (セーフ モードなど)](https://support.microsoft.com/help/17076/windows-8-startup-settings-safe-mode)」を参照してください。

> [!NOTE]
> このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。 また、**onetimeadvancedoptions** を使用して、次回の起動時に [詳細オプション] (**F8** キー) メニュー (**Legacy**) を 1 回使用することもできます。

**bootstatuspolicy** *policy*

ブート状態ポリシーを制御します。 ブート状態 "*ポリシー*" は、次のいずれかにすることができます。

- `DisplayAllFailures`:起動の失敗、シャットダウンの失敗、またはチェックポイントの失敗があった場合に、すべてのエラーを表示します。 コンピューター再起動時に Windows 回復環境へフェールオーバーします。

- `IgnoreAllFailures`:起動の失敗、シャットダウンの失敗、またはチェックポイントの失敗があった場合に、すべてのエラーを無視します。 エラー発生後、コンピューターの通常どおりの起動が試みられます。

- `IgnoreShutdownFailures`:シャットダウンに失敗した場合にのみ、エラーを無視します。 シャットダウンに失敗した場合、コンピューター再起動時に Windows 回復環境へ自動的にフェールオーバーしません。 これは Windows 8 の既定の設定です。

- `IgnoreBootFailures`:起動に失敗した場合にのみ、エラーを無視します。 起動に失敗した場合、コンピューター再起動時に Windows 回復環境へ自動的にフェールオーバーしません。

- `IgnoreCheckpointFailures`:チェックポイントが失敗した場合にのみ、エラーを無視します。 失敗したチェックポイントがある場合、コンピューター再起動時に Windows 回復環境へ自動的にフェールオーバーしません。 このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

- `DisplayShutdownFailures`:失敗したシャットダウンがある場合は、エラーを表示します。 シャットダウンが失敗した場合、コンピューター再起動時に Windows 回復環境へフェールオーバーします。 起動の失敗と失敗したチェックポイントを無視します。 このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

- `DisplayBootFailures`:起動が失敗した場合は、エラーを表示します。 起動が失敗した場合、コンピューター再起動時に Windows 回復環境へフェールオーバーします。 シャットダウンの失敗と失敗したチェックポイントを無視します。 このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

- `DisplayCheckpointFailures`:失敗したチェックポイントがある場合は、エラーを表示します。 失敗したチェックポイントがある場合、コンピューター再起動時に Windows 回復環境へフェールオーバーします。 起動およびシャットダウンの失敗を無視します。 このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

**bootux** \[ **disabled** | **basic** | **standard** \]  
起動画面のアニメーションを制御します。 有効な値は、disabled、basic、standard です。

> [!NOTE]
> Windows 8 および Windows Server 2012 ではサポートされていません。

**disabledynamictick** \[ **yes** | **no** \]  
動的タイマー ティック機能を有効または無効にします。 

> [!NOTE]
> このオプションは、デバッグのためにのみ使用してください。

**disableelamdrivers** \[ **yes** | **no** \]  
起動時マルウェア対策 (ELAM) ドライバーの読み込みを制御します。 セキュリティ上の理由から、このエントリは OS ローダーによって削除されます。 このオプションは、F8 メニューを使用することによってのみトリガーできます。 このオプションをトリガーするには、だれかが (コンピューターに) 物理的に存在している必要があります。

> [!NOTE]
> このオプションは、デバッグのためにのみ使用してください。 

**forcelegacyplatform** \[ **yes** | **no** \]  
OS で CMOS やキーボード コントローラーなどのレガシ PC デバイスの存在が強制的に想定されるようにします。

> [!NOTE]
> このオプションは、デバッグのためにのみ使用してください。 

**groupsize** *maxsize*: 1 つのプロセッサ グループに含まれる論理プロセッサの最大数を設定します。ここで *maxsize* は、1 から 64 まで (両端を含む) の 2 の累乗です。 既定では、プロセッサ グループの最大サイズは 64 論理プロセッサです。 このブート構成設定を使用して、テスト目的でコンピューターのプロセッサ グループのサイズと構成をオーバーライドすることができます。 [プロセッサ グループ](https://docs.microsoft.com/windows/win32/procthread/processor-groups)では、64 を超える数の論理プロセッサを搭載したコンピューターがサポートされます。 このブート オプションは、64 ビット版の Windows 7 および Windows Server 2008 R2 以降のバージョンで使用できます。 このブート オプションは、32 ビット版の Windows 7 には無効です。

**groupsize** オプションは、複数のグループに強制的に適用する必要があり、コンピューターのアクティブな論理プロセッサが 64 個以下である場合に使用します。 このオプションの使用方法の詳細については、「[ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-test-drivers-for-multiple-processor-group-support)」を参照してください。

**groupaware** \[ **on** | **off** \]  
複数のプロセッサ グループがある環境において、複数のグループをドライバーに強制的に認識させます。 このオプションを使用すると、グループ間のドライバーとコンポーネントの非互換性を明らかにするのに役立ちます。 [プロセッサ グループ](https://docs.microsoft.com/windows/win32/procthread/processor-groups)では、64 を超える数の論理プロセッサを搭載したコンピューターがサポートされます。 このブート オプションは、64 ビット版の Windows 7 および Windows Server 2008 R2 以降のバージョンで使用できます。 このブート オプションは、32 ビット版の Windows 7 には無効です。 **groupaware** オプションと **groupsize** オプションを使用すると、コンピューターのアクティブな論理プロセッサが 64 個以下である場合に、複数のグループで機能するようにドライバーの互換性をテストできます。

**groupaware on** に設定すると、プロセスは確実にグループ 0 以外のグループで開始されます。 これにより、ドライバーとコンポーネントの間でグループ間の相互作用が生じる可能性が高くなります。 また、このオプションを選択すると、レガシ関数である **KeSetTargetProcessorDpc**、**KeSetSystemAffinityThreadEx**、**KeRevertToUserAffinityThreadEx** の動作が変更され、アクティブな論理プロセッサを含む最も大きい番号のグループで常に操作が実行されるようになります。 これらのレガシ関数のいずれかを呼び出すドライバーは、対応するグループ対応関数 (**KeSetTargetProcessorDpcEx**、**KeSetSystemGroupAffinityThread**、**KeRevertToUserGroupAffinityThread**) を呼び出すように変更する必要があります。

このオプションの使用方法の詳細については、「[ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-test-drivers-for-multiple-processor-group-support)」を参照してください。

**hal** *file*: 代替の HAL ファイルを読み込むようにオペレーティング システム ローダーに指示します。 指定されたファイルは %SystemRoot%\\system32 ディレクトリに存在する必要があります。

**hypervisorbusparams** *Bus.Device.Function*  
デバッグ デバイスの PCI バス、デバイス、関数の番号を定義します。 たとえば、1.5.0 は、バス 1、デバイス 5、関数 0 のデバッグ デバイスを表します。 このオプションは、デバッグ用に 1394 ケーブルか USB 2.0 または USB 3.0 デバッグ ケーブルを使用している場合に使用します。

**hypervisordebug** \[ **On** | **Off** \]  
ハイパーバイザー デバッガーが有効かどうかを制御します。

**シリアル**  
デバッグ用のシリアル接続を指定します。 **Serial** オプションを指定した場合は、**hypervisordebugport** オプションと **hypervisorbaudrate** オプションも設定します。

``` syntax
bcdedit /set hypervisordebugtype serial
bcdedit /set hypervisordebugport 1
bcdedit /set hypervisorbaudrate 115200
bcdedit /set hypervisordebug on
bcdedit /set hypervisorlaunchtype auto
```

**1394**  
デバッグ用の IEEE 1394 (FireWire) 接続を指定します。 このオプションを使用する場合は、**hypervisorchannel** オプションも設定する必要があります。

> [!IMPORTANT]
> 1394 トランスポートは、Windows 10 バージョン 1607 およびそれ以前で使用できます。 それより後のバージョンの Windows では使用できません。 イーサネットを使用して KDNET などの他のトランスポートにプロジェクトを移行する必要があります。 そのトランスポートの詳細については、「[KDNET ネットワーク カーネル デバッグの自動設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)」を参照してください。


**Net**  
デバッグ用のイーサネット ネットワーク接続を指定します。 このオプションを使用する場合は、**hypervisorhostip** オプションも設定する必要があります。

**hypervisorhostip** *IP address* (**hypervisordebugtype** が **Net** の場合にのみ使用されます)。ネットワーク接続経由でハイパーバイザーをデバッグする場合は、ホスト デバッガーの IPv4 アドレスを指定します。 Hyper-V のデバッグの詳細については、「[Hyper-V による仮想マシンの作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)」を参照してください。

**hypervisorhostport** \[ *port* \]  
(**hypervisordebugtype** が **Net** の場合にのみ使用されます。) ネットワーク デバッグの場合は、ホスト デバッガーの通信ポートを指定します。 49152 以上である必要があります。

**hypervisordhcp** \[ **yes** | **no** \]  
ハイパーバイザーで使用するネットワーク デバッガーによる DHCP の使用を制御します。 これを **no** に設定すると、強制的に自動プライベート IP アドレス指定 (APIPA) を使用してローカル リンク IP アドレスが取得されます。

**hypervisoriommupolicy** \[ **default** | **enable** | **disable**\]  
ハイパーバイザーで入出力メモリ管理ユニット (IOMMU) を使用するかどうかを制御します。

**hypervisorlaunchtype** \[ **Off** | **Auto** \]  
ハイパーバイザー起動オプションを制御します。 対象のコンピューターで Hyper-V をデバッグするようにデバッガーを設定する場合は、このオプションをターゲット コンピューターで **Auto** に設定します。 詳細については、「[Hyper-V による仮想マシンの作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)」を参照してください。

**hypervisorloadoptions NOFORCESNOOP** \[ **Yes** | **No** \]  
ハイパーバイザーでシステムの IOMMU にスヌープ制御を強制的に適用するかどうかを指定します。

**hypervisornumproc** *number*  
ハイパーバイザーで開始できる論理プロセッサの合計数を指定します。

**hypervisorrootproc** *number*  
ルート パーティション内の仮想プロセッサの最大数を指定し、ハイパーバイザーで論理プロセッサを開始できる分割後の NUMA (Non-Uniform Memory Architecture) ノードの数を制限します。

**hypervisorrootprocpernode** *number*  
分割前の NUMA (Non-Uniform Memory Architecture) ノード内で開始できる、ルート パーティション内の仮想プロセッサの合計数を指定します。

**hypervisorusekey** \[ *key* \]  
(**hypervisordebugtype** が **Net** の場合にのみ使用されます。) ネットワーク デバッグの場合、接続の暗号化に使用するキーを指定します。 使用できるのは \[0 - 9\] および \[a - z\] のみです。

**hypervisoruselargevtlb** \[ **yes** | **no**: 仮想変換ルックアサイド バッファー (TLB) のサイズを増やします。

**increaseuserva** *Megabytes*: ユーザー モードの仮想アドレス空間のメモリ量を MB 単位で指定します。

Windows の 32 ビット版では、アプリケーションで 4 GB の仮想アドレス空間を使用できます。 仮想アドレス空間は、2 GB をアプリケーションで使用できるように分割され、他の 2 GB はシステムでのみ使用できます。

**increaseuserva** オプションで有効になる 4 GB のチューニング機能を使用すると、アプリケーションで使用可能な仮想アドレス空間を最大 3 GB まで増やすことができます。これにより、システムで使用可能な量は 1 GB から 2 GB の間にまで減ります。 **BCEdit /set increaseuserva** *Megabytes* コマンドでは、10 進表記で 2048 (2 GB) から 3072 (3 GB) MB までの任意の値を指定できます。 残りのアドレス空間 (4 GB から指定した量を引いたもの) が Windows でカーネル モードのアドレス空間として使用されます。

この機能の詳細については、「[4 GB のチューニング (Windows)](https://docs.microsoft.com/windows/desktop/Memory/4-gigabyte-tuning)」を参照してください。

**kernel** *file*: 代替カーネルを読み込むようにオペレーティング システムに指示します。 指定されたファイルは %SystemRoot%\\system32 ディレクトリに存在する必要があります。

**loadoptions busparams**=*Bus.Device.Function*: 複数のコントローラーが存在する場合にターゲット コントローラーを指定します。 この構文は、デバッグ用に 1394 ケーブルまたは USB 2.0 デバッグ ケーブルを使用する場合に適しています。 *Bus* でバス番号、*Device* でデバイス番号、*Function* で関数番号を指定します。

> [!NOTE]
> 1394 デバッグでは、構成する Windows のバージョンに関係なく、バス パラメーターを 10 進数で指定する必要があります。 USB 2.0 デバッグに使用するバス パラメーターの形式は、Windows のバージョンによって異なります。 Windows Server 2008 では、USB 2.0 バスパラメーターを 16 進数で指定する必要があります。 Windows 7 および Windows Server 2008 R2 以降のバージョンの Windows では、USB 2.0 バス パラメーターを 10 進数で指定する必要があります。

**maxgroup** \[ **on** | **off** \]  
プロセッサ グループ構成で作成されるグループの数を最大化します。

**maxgroup on** に設定すると、特定のコンピューターのグループ数が最大化されるように NUMA ノードをグループに割り当てることができます。 作成されるグループの数は、コンピューターの NUMA ノードの数、またはこのバージョンの Windows でサポートされているグループの最大数のいずれか小さい方です。 既定の動作 (**maxgroup off)** では、NUMA ノードをできるだけ少ないグループにまとめてパックします。

複数のグループを使用するとき、コンピューターのアクティブな論理プロセッサが 64 個以下で、コンピューターに複数の NUMA ノードが既に存在する場合に、このオプションを使用します。 このオプションを使用すると、64 を超える数の論理プロセッサを搭載したコンピューターの既定のグループ構成を変更することもできます。

[プロセッサ グループ](https://docs.microsoft.com/windows/desktop/ProcThread/processor-groups)では、64 を超える数の論理プロセッサを搭載したコンピューターがサポートされます。 このオプションは、64 ビット版の Windows 7 および Windows Server 2008 R2 以降のバージョンで使用できます。 このブート オプションは、32 ビット版の Windows 7 には無効です。

このオプションの使用方法の詳細については、「[ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター](boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)」を参照してください。

**nointegritychecks** \[ **on** | **off** \]: 整合性チェックを無効にします。 セキュア ブートが有効な場合は設定できません。 この値は、Windows 7 および Windows 8 では無視されます。

**nolowmem** \[ **on** | **off** \]: 下位メモリの使用を制御します。 **nolowmem on** を指定した場合、このオプションが選択されるとオペレーティング システム、デバイス ドライバー、すべてのアプリケーションが 4 GB 境界より上のアドレスに読み込まれ、すべてのメモリ プールが Windows によって 4 GB 境界より上のアドレスに割り当てられるようになります。 **nolowmem** オプションは、Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows では無視されることにご注意ください。

**novesa** \[ **on** | **off** \]: VGA ドライバーで VESA BIOS 呼び出しを回避する必要があるかどうかを示します。 Windows 8 と Windows Server 2012 では、このオプションは無視されます。

**novga** \[ **on** | **off** \]: OS での VGA モードの使用が無効になります。 このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

**nx** \[**Optin |OptOut | AlwaysOn |AlwaysOff**\]  
データ実行防止 (DEP) を有効化、無効化、構成します。DEP は、保護されたメモリの場所で有害なコードが実行されないように設計された、一連のハードウェア テクノロジとソフトウェア テクノロジです。 DEP 設定の詳細については、「[データ実行防止](https://docs.microsoft.com/windows/desktop/Memory/data-execution-prevention)」を参照してください。

**Optin**  
Windows カーネルとドライバーを含むオペレーティング システム コンポーネントに対してのみ DEP を有効にします。 管理者は、Application Compatibility Toolkit (ACT) を使用して、選択した実行可能ファイルに対して DEP を有効にすることができます。

**Optout**  
オペレーティング システムおよび Windows カーネルとドライバーを含むすべてのプロセスに対して DEP を有効にします。 ただし、管理者は **[コントロール パネル]** の **[システム]** を使用して、選択した実行可能ファイルの DEP を無効にすることができます。

**AlwaysOn**  
オペレーティング システムおよび Windows カーネルとドライバーを含むすべてのプロセスに対して DEP を有効にします。 DEP を無効にしようとする試みは、すべて無視されます。

**AlwaysOff**  
DEP を無効にします。 DEP を選択的に有効にしようとしても無視されます。

Windows Vista では、このパラメーターによって物理アドレス拡張 (PAE) も無効になります。 Windows Server 2008 では、このパラメーターを指定しても PAE は無効になりません。

**onecpu** \[ **on** | **off** \]  
複数の論理プロセッサを持つコンピューターで、強制的にブート CPU のみを使用します。

たとえば、次のコマンドは、現在のオペレーティング システム ローダーで 1 つのプロセッサを使用するように構成します。

```syntax
bcdedit /set onecpu on
```

**onetimeadvancedoptions** \[ **on** | **off** \]  
次回の起動時に、システムをレガシ メニュー (F8 メニュー) で起動するかどうかを制御します。

> [!NOTE]
> このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

```syntax
bcdedit /set {current} onetimeadvancedoptions on
```

**pae** \[ **Default** | **ForceEnable** | **ForceDisable** \]  
物理アドレス拡張 (PAE) を有効または無効にします。 PAE を有効にすると、システムに Windows カーネルの PAE バージョンが読み込まれます。

**pae** パラメーターは、x86 ベースおよび x64 ベースのプロセッサを搭載したコンピューターで実行される 32 ビット版の Windows のブート エントリでのみ有効です。 32 ビット版の Windows (Windows 8 より前) では、PAE は既定で無効になっています。 ただし、静的リソース アフィニティ テーブル (SRAT) で定義された 4 GB 領域を超えるメモリ範囲でコンピューターがホットアド メモリ デバイス用に構成されている場合は、Windows で自動的に PAE が有効になります。 "*ホットアド メモリ*" では、コンピューターの再起動や電源オフを行うことなく追加できるメモリ デバイスがサポートされます。 この場合、システムの起動時に PAE を有効にする必要があるため、再起動と再起動の間に追加された拡張メモリにシステムがすぐに対応できるように、PAE が自動的に有効になります。 ホットアド メモリは、Windows Server 2008 Datacenter Edition および Windows Server 2008 for Itanium-Based Systems と、以降のすべてのバージョンの Windows Server Datacenter Edition および Enterprise Edition でのみサポートされています。 さらに、Windows Server 2008 より前のバージョンの Windows では、ホットアド メモリは、ACPI BIOS、x86 プロセッサ、および特殊なハードウェアを搭載したコンピューターでのみサポートされています。 Windows Server 2008 以降のバージョンの Windows Server の場合、すべてのプロセッサ アーキテクチャでサポートされています。

ハードウェア対応のデータ実行防止 (DEP) をサポートし、DEP がサポートされている 32 ビット版の Windows オペレーティング システムを実行するコンピューターでは、DEP が有効になっていると、PAE が自動的に有効になります。また、すべての 32 ビット版の Windows オペレーティング システム (Windows Server 2003 SP1 を除く) では、DEP を無効にすると、PAE は無効になります。 DEP が無効になっているときに PAE を有効にするには、 **/set nx AlwaysOff** と **/set pae ForceEnable** を使用して、PAE を明示的に有効にする必要があります。 DEP の詳細については、「[DEP と PAE を構成するためのブート パラメーター](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-configure-dep-and-pae)」を参照してください。

**pae** パラメーターと、PAE 構成に影響するその他のパラメーターの使用方法の詳細については、「[DEP と PAE を構成するためのブート パラメーター](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-configure-dep-and-pae)」を参照してください。

**pciexpress** \[ **default** | **forcedisable**\]  
PCI Express 機能を有効または無効にします。 コンピューター プラットフォームで PCI Express 機能がサポートされていて、ACPI \_OSC メソッドによって機能の制御がオペレーティング システムに許可されている場合、Windows で PCI Express ネイティブ コントロール機能を使用して高度な機能が有効化されます (これが既定です)。 **forcedisable** オプションは、PCI Express の高度な機能を無効にし、レガシ PCI Express の動作を使用する場合に使用します。 詳細については、「[Windows での PCI Express ネイティブ コントロールの有効化](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn631753(v=vs.85))」を参照してください。

**quietboot** \[ **on** | **off** \]  
Windows 起動画面の表示とアニメーションの代わりの高解像度ビットマップの表示を制御します。 Windows Vista より前のオペレーティング システムでは、 **/noguiboot** によって同様の機能が提供されます。

> [!NOTE]
> Windows 8 では **quietboot** オプションを使用しないでください。使用すると、すべてのブート グラフィックスだけでなくバグ チェック データも表示されなくなります。

**removememory** *Megabytes*: オペレーティング システムで使用できる使用可能メモリの合計からメモリを削除します。

たとえば、次のコマンドは、指定されたブート エントリに関連付けられた、オペレーティング システムで使用可能なメモリの合計から 256 MB のメモリを削除します。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} removememory 256
```

**sos** \[ **on** | **off** \]  
ドライバーがブート プロセス中に読み込まれるときのドライバーの名前の表示を制御します。 名前を表示するには **sos on** を使用します。 表示を抑制するには、**sos off** を使用します。

**testsigning** \[ **on** | **off** \]  
Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008、または Windows Vista で、テスト署名された任意の種類のカーネル モード コードを読み込むかどうかを制御します。 このオプションは既定では設定されていません。つまり、64 ビット版の Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008、Windows Vista でテスト署名されたカーネル モード ドライバーは、既定では読み込まれません。 BCDEdit コマンドを実行した後、コンピューターを再起動して変更を有効にします。 詳細については、「[テスト署名の概要](https://docs.microsoft.com/windows-hardware/drivers/install/introduction-to-test-signing)」を参照してください。

> [!NOTE]
> BCDEdit のオプションを設定する前に、コンピューターで BitLocker とセキュア ブートを無効にするか中断することが必要になる場合があります。

**tpmbootentropy** \[ **default** | **ForceEnable** | **ForceDisable**\]  
オペレーティング システムの乱数ジェネレーターのシードを設定するために、トラステッド プラットフォーム モジュール (TPM) からエントロピを収集するかどうかを決定します。

**truncatememory** *address*: Windows で使用可能な物理メモリの量を制限します。 このオプションを使用すると、指定した物理アドレス以上のすべてのメモリが Windows で無視されます。 *address* はバイト単位で指定します。

たとえば、次のコマンドは、物理アドレスの上限を 1 GB に設定します。 アドレスは 10 進数 (1073741824) または 16 進数 (0x40000000) で指定できます。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} truncatememory 0x40000000
```

**tscsyncpolicy** \[ **Default** | **Legacy** | **Enhanced** \]  
タイムスタンプ カウンターの同期ポリシーを制御します。 このオプションは、デバッグのためにのみ使用してください。

> [!NOTE]
> このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

**usefirmwarepcisettings** \[ **yes** | **no** \]  
BIOS で構成されている PCI (Peripheral Component Interconnect) リソースの使用を有効または無効にします。

**useplatformclock** \[ **yes** | **no** \]  
プラットフォーム クロックをシステムのパフォーマンス カウンターとして強制的に使用します。

> [!NOTE]
> このオプションは、デバッグのためにのみ使用してください。

**uselegacyapicmode** \[ **yes** | **no** \]  
プロセッサとチップセットが拡張 APIC モードをサポートしている場合でも、レガシ APIC モードを強制するために使用します。

**useplatformtick** \[ **yes** | **no** \]  
プラットフォーム ソースによってクロックが強制的にサポートされるようにします。合成タイマーは許可されません。 このオプションは、Windows 8 および Windows Server 2012 以降で使用できます。

> [!NOTE]
> このオプションは、デバッグのためにのみ使用してください。

**vga** \[ **on** | **off** \]  
安全な解像度を強制的に使用します。 たとえば、Windows 7 を実行しているコンピューターでは、このオプションを使用すると 640 x 480 の解像度が強制的に使用されます。 Windows 8 を実行しているコンピューターでは、このオプションを使用すると、使用可能な場合は 800 x 600 の解像度、そうでない場合は 640 x 480 が使用されます。

**xsavedisable** \[ **0** | **1** \]  
ゼロ (0) 以外の値に設定すると、カーネルの XSAVE プロセッサ機能が無効になります。

**x2apicpolicy** \[ **enable** | **disable** \]  
拡張 APIC モードの使用を有効または無効にします (サポートされている場合)。 既定では、使用可能な場合は拡張 APIC モードが使用されます。

### <a name="comments"></a>備考

特定の BCD 要素とブート オプションの詳細を表示するには、次のコマンドを使用します。**BCDEdit /?OSLOADER** および **BCDEdit/? TYPES OSLOADER**

現在のブート エントリとその設定を表示するには、**bcdedit /enum** コマンドを使用します。 このコマンドにより、アクティブなブート エントリと、エントリに関連付けられているグローバル一意識別子 (GUID) が表示されます。 その識別子を **/set** コマンドで使用して、特定のブート エントリのオプションを構成します。

設定したブート オプションの値を削除するには、 **/deletevalue** オプションを使用します。 このコマンドの構文は次のとおりです。

**bcdedit** /**deletevalue** \[ **{ID}** \] *datatatype*

たとえば、**groupsize** というプロセッサ グループ オプションをテスト目的で新しい値に変更した場合は、次のコマンドを入力してコンピューターを再起動することで、既定値の 64 に戻すことができます。

``` syntax
bcdedit /deletevalue groupsize
```

ブート オプションに対するどのような変更も、有効にするには再起動することが必要です。 一般的に使用される BCDEdit コマンドの詳細については、「[ブート構成データ エディターに関してよく寄せられる質問](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc721886(v=ws.10))」を参照してください。

## <a name="requirements"></a>要件

**サポートされている最小のクライアント**:Windows Vista

**サポートされている最小のサーバー**:Windows Server 2008

****: 


## <a name="see-also"></a>関連項目

- [BCDEdit /deletevalue](bcdedit--deletevalue.md)
