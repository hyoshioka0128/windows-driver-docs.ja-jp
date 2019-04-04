---
title: レポート検証
description: レポート検証
ms.assetid: 3731C877-1A69-447C-A5DB-0BDD1B753D3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb593fc74a083374d58f4da6d0d6b327f02df909
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572165"
---
# <a name="storport-verification"></a>レポート検証


## <span id="ddk_storport_verification_tools"></span><span id="DDK_STORPORT_VERIFICATION_TOOLS"></span>


Storport の検証の機能は、ポート ドライバー、Storport ミニポート ドライバーとの対話を監視します。 ルーチン、ミニポート ドライバー誤っていない正しくまたは応答する要求をポート ドライバーから、過剰な要求に応答する時間のかかるバグ チェックが発行されます。

**注**  Storport の検証の機能は Windows Vista および Windows の以降のバージョンで使用できます。

 

### <a name="span-idviolationsdetectedbystorportverificationspanspan-idviolationsdetectedbystorportverificationspanviolations-detected-by-storport-verification"></a><span id="violations_detected_by_storport_verification"></span><span id="VIOLATIONS_DETECTED_BY_STORPORT_VERIFICATION"></span>Storport の確認によって検出された違反

Storport の検証の機能は、Storport ルーチンのいくつか誤ってを検出できます。 これらのチェックの一部を個別に無効にすることもできます。

Storport の検証の機能では、バグ チェック 0xF1 またはバグ チェック 0xC4 Storport ミニポート ドライバーが次の違反のいずれかのコミットされた場合に発行します。

-   ミニポート ドライバーに渡します (NULL ポインター) の無効な引数、 [ **StorPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff567108)ルーチン。

-   ミニポート ドライバー呼び出し[ **StorPortStallExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff567508)失速プロセッサ時間の過度の長さを 0.1 秒より長い遅延を指定します。

-   [**StorPortFreeDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff567061)ミニポート ドライバーからのみ呼び出すことができます**HwStorFindAdapter**ルーチン。

-   [**StorPortGetUncachedExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff567103)ミニポート ドライバーからのみ呼び出すことができます**HwStorFindAdapter**ルーチン バス マスター アダプターに対してのみ呼び出すことができます。 ミニポートを設定する必要があります、 **SrbExtensionSize**の[ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff557459) を呼び出す前に(Storport)構造**StorPortGetUncachedExtension**します。

-   [ **StorPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff567080)ルーチンには、システムのプラグ アンド プレイ (PnP) マネージャーで、ドライバーに割り当てられているアドレスのみがサポートしています。

-   ミニポート ドライバーのいずれかに無効な仮想アドレスを通過する、**StorPortRead * * * xxx*または **StorPortWrite * * * xxx*ルーチン (たとえば、 [ **StorPortReadRegisterUchar** ](https://msdn.microsoft.com/library/windows/hardware/ff567483)または[ **StorPortWritePortBufferUlong**](https://msdn.microsoft.com/library/windows/hardware/ff567517))。 通常は、指定されたアドレスは、一般的なバッファー領域にマップされません。 指定した*登録*または*ポート*によって返されるメモリ領域の割り当てられた範囲内で指定する必要があります[ **StorPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff567080)ルーチン。 このチェックは、x86 ベースのシステムでのみサポートされます。

Storport の検証を使用するバグの検査パラメーターの一覧は、次を参照してください。 [**バグ チェック 0xF1** ](https://msdn.microsoft.com/library/windows/hardware/ff560365) (SCSI\_VERIFIER\_検出\_違反)。 バグ チェック 0xF1、Storport の検証も使用だけでなく[**バグ チェック 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (ドライバー\_VERIFIER\_検出\_違反)。

**注**  [**バグ チェック 0xF1** ](https://msdn.microsoft.com/library/windows/hardware/ff560365) SCSI 検証および Storport の検証の両方に使用されます。

 

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

Storport の確認オプションをアクティブ化するための手順は他の Driver Verifier のオプションがアクティブ化するためのプロシージャから異なります。

**Storport の検証をアクティブ化するには**

1.  ドライバー検証マネージャーを使用して、または*Verifier.exe*コマンドライン、ミニポート ドライバーの検証を開始します。 Storport の検証はオプションとして利用できない、ために、少なくとも 1 つを選択する必要があります*他*Driver Verifier のオプション。 詳細については、[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)と[検証するドライバーを選択すると](selecting-drivers-to-be-verified.md)を参照してください。

2.  使用して、レジストリを開く*regedit.exe*します。 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\StorPort**キーを追加するという名前のサブキー**検証ツール**. 場合、 **StorPort**キーが存在しないか、それを作成する必要があります。 内で、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\STORPort\\Verifier**キーの追加、 **REG\_DWORD**という名前のエントリ**VerifyLevel**します。 Storport の検証テストをアクティブになるこのエントリに割り当てられた値が決定されます。 0x1 の値では、最大の検証を提供します。

3.  コンピューターを再起動します。

場合、 **VerifyLevel**値が存在しないか 0 xffffffff と等しく、Storport の検証が無効になります。

### <a name="span-idactivatingwithoutrebootingspanspan-idactivatingwithoutrebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>再起動しなくてもアクティブ化します。

一般に、アクティブ化または再起動 (リブート) することがなく、Storport の検証を非アクティブ化できません任意の Windows オペレーティング システム上のコンピューター。 *StorPort.sys*ドライバーの読み込み、 **VerifyLevel**これは、通常ブート時にレジストリ エントリ、読み込み時にのみです。 ただし場合、 *StorPort.sys*レジストリ エントリを追加するかアンロードし、再読み込み場合は、コンピューターを再起動せずに Windows Vista 以降のバージョンの Windows で Storport 検証が有効にすることができます、ドライバーが読み込まれていません。

 

 





