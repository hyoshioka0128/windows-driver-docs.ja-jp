---
title: 仮想プロビジョニング
description: 仮想プロビジョニング
ms.assetid: 0D65DDCC-D207-4EA8-B5D6-56DF57221EE3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51beda233bada2573181343ee359a17f8c4f3c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340910"
---
# <a name="thin-provisioning"></a>仮想プロビジョニング


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


仮想プロビジョニングとは、エンド ツー エンドのストレージ ソリューションをプロビジョニングします。 これは、ホストとクライアント アプリケーションでストレージのデプロイと実行の計画が必要です。 Windows Server のシン プロビジョニング機能は、シン プロビジョニング対応記憶域と、ホスト サーバー間のインターフェイスとして機能します。 シン プロビジョニング機能には、シン プロビジョニング論理ユニット (LUN) の識別、しきい値通知、リソースの枯渇のハンドルとエンドユーザーにサービスをプロビジョニングするスケーラブルな高可用性の記憶域を提供するための領域の解放が含まれます。

## <a name="span-idthinprovisioninglunidentificationspanspan-idthinprovisioninglunidentificationspanspan-idthinprovisioninglunidentificationspanthin-provisioning-lun-identification"></a><span id="Thin_Provisioning_LUN_Identification"></span><span id="thin_provisioning_lun_identification"></span><span id="THIN_PROVISIONING_LUN_IDENTIFICATION"></span>シン プロビジョニング LUN の識別


Windows Server では、Windows Server 2012 以降でシン プロビジョニングの Lun を識別するための T10 SCSI ブロック コマンド 3 (SBC3) 標準仕様を採用しています。 初期ターゲット デバイスの列挙中には、Windows Server は、ターゲット デバイスからすべてのプロパティのパラメーターを収集します。 Windows Server では、プロビジョニングの種類および UNMAP とトリミング機能を識別します。 記憶域デバイスでは、そのプロビジョニングの種類とマッピング解除と SBC3 仕様によるトリミング機能を報告します。

ストレージ デバイスがその現在の機能を正確に報告しない場合、デバイスの互換性の問題は発生します。 たとえば、ストレージ デバイスを報告しますマッピング解除コマンドをサポートして UNMAP のコマンドは、サポートしていませんが、ディスク形式のハング問題が発生します。 プロビジョニングの種類の情報が正確で、記憶域スタックが優れた I/O が記憶域のプロビジョニングの種類に従って処理を提供できます。

## <a name="span-idrun-timeprovisioningtypeorluncapacitychangesspanspan-idrun-timeprovisioningtypeorluncapacitychangesspanspan-idrun-timeprovisioningtypeorluncapacitychangesspanrun-time-provisioning-type-or-lun-capacity-changes"></a><span id="Run-time_Provisioning_Type_or_LUN_Capacity_Changes"></span><span id="run-time_provisioning_type_or_lun_capacity_changes"></span><span id="RUN-TIME_PROVISIONING_TYPE_OR_LUN_CAPACITY_CHANGES"></span>実行時プロビジョニングの種類または LUN の容量の変更


記憶域管理者には、プロビジョニングの種類または LUN の容量を変更できます。 プロビジョニングの種類または LUN の容量を変更すると、記憶域配列をセンス データが要求されたときに、正しい情報を返すユニットの注意の意味条件が発生します。 Windows Server では、プロビジョニングの種類または LUN の容量の変更のシステム管理者に警告をシステム イベントを記録します。

## <a name="span-idthresholdandresourceexhaustionhandlesspanspan-idthresholdandresourceexhaustionhandlesspanspan-idthresholdandresourceexhaustionhandlesspanthreshold-and-resource-exhaustion-handles"></a><span id="Threshold_and_Resource_Exhaustion_Handles_"></span><span id="threshold_and_resource_exhaustion_handles_"></span><span id="THRESHOLD_AND_RESOURCE_EXHAUSTION_HANDLES_"></span>しきい値とリソース枯渇のハンドル


シン プロビジョニング LUN は、通常、LUN のサイズよりも少ない物理ディスク領域が作成されます。 しきい値通知は、必要なストレージ領域の消費状態のホストとクライアント アプリケーションのアラートを生成する関数です。 シン プロビジョニング ストレージ アレイの多くは、しきい値に達したときにイベントを報告しません。 これらのシン プロビジョニング記憶域ソリューションでは、その独自のストレージ管理ユーティリティを使ってしきい値通知を解決します。 そのため、ホストとクライアント アプリケーションで、これらの記憶域配列のレポートに永続的なリソース枯渇がある唯一のイベントです。 シン プロビジョニング ストレージ デバイスが一時的リソース枯渇のハンドル、しきい値通知ハンドルを使用したり、アラート システム管理者または記憶域スペースの消費量と、クライアント アプリケーションに永続的なリソース枯渇のハンドルに近づいています容量。

### <a name="span-idthinprovisioningthresholdnotificationspanspan-idthinprovisioningthresholdnotificationspanspan-idthinprovisioningthresholdnotificationspanthin-provisioning-threshold-notification"></a><span id="Thin_Provisioning_Threshold_Notification"></span><span id="thin_provisioning_threshold_notification"></span><span id="THIN_PROVISIONING_THRESHOLD_NOTIFICATION"></span>シン プロビジョニングしきい値通知

記憶域の管理ユーティリティは、シン プロビジョニングのしきい値を設定します。 Windows Server では、記憶域の管理ユーティリティによって設定されたしきい値を上書きしません。 シン プロビジョニングの LUN、記憶域管理者が、平均ストレージ使用量レートに基づいてしきい値を指定してください。 書き込みコマンドが記憶域のターゲット デバイスが設定したしきい値を超える場合にターゲット デバイスは検出データを使用してコマンドを終了し、"シン プロビジョニング ソフトしきい値に達しました"というメッセージを送信します。 Windows サーバーでは、一致したセンス データを受信すると、以下の処理が行われます。

-   システム イベントは、LUN のデバイスでリソースの使用状況または可用性のしきい値に達したホストの管理者に警告に記録されます。
-   システム イベント ログにターゲット デバイスのログ ページからおよび使用可能な割り当てられたリソースに関する情報が報告します。 これを行うには、記憶域配列はの論理ブロックは、Windows Server システムのイベントを生成するためにプロビジョニングのログ ページ仕様をサポートする必要があります。
-   終了コマンドが再試行されます。

**注**  場合このエラーが記録された後に送信されたコマンドが失われる可能性のある記述ファイル\_フラグ\_書き込み\_を通じて永続的なリソース枯渇の条件をトリガーする可能性があるために設定されていません。

 

### <a name="span-idtemporaryresourceexhaustionspanspan-idtemporaryresourceexhaustionspanspan-idtemporaryresourceexhaustionspantemporary-resource-exhaustion"></a><span id="Temporary_Resource_Exhaustion"></span><span id="temporary_resource_exhaustion"></span><span id="TEMPORARY_RESOURCE_EXHAUSTION"></span>一時的リソース枯渇

記憶域配列により、自動拡張、LUN 上の関数、管理者は、一時的リソース枯渇の通知を使用して、ストレージ デバイスが 4 秒以内、LUN に追加の領域を割り当てられることを確認します。 書き込みコマンドでは、一時的リソース枯渇の条件が発生するときに、記憶域デバイスにコマンドを検出データを使用して、操作を要求し、"領域割り当て IN PROGRESS"メッセージが返されますが終了します。 一時的リソース枯渇は、次のように処理されます。

-   1 秒に設定する再試行の間隔で 4 回、元の要求を再試行してください。
-   すべての再試行が失敗した場合は、アプリケーションに、要求が失敗しました。
-   ストレージ デバイスが一時的リソース枯渇を処理しない場合、Windows Server には、永続的なリソース枯渇の状態を返すことによって、次の書き込み要求が失敗する記憶装置が期待しています。

### <a name="span-idpermanentresourceexhaustionspanspan-idpermanentresourceexhaustionspanspan-idpermanentresourceexhaustionspanpermanent-resource-exhaustion"></a><span id="Permanent__Resource_Exhaustion"></span><span id="permanent__resource_exhaustion"></span><span id="PERMANENT__RESOURCE_EXHAUSTION"></span>永続的なリソース枯渇

永続的なリソース枯渇の条件では、シン プロビジョニングの LUN、記憶域の最大領域の上限に達したことを示します。 書き込みコマンドで永続的なリソース枯渇が発生したときに記憶装置はセンス データを使用して、操作を終了し、「領域の割り当てに失敗しました書き込み保護する」のメッセージを送信します。 永続的な消費は次のように処理されます。

-   元の要求ファイルが含まれる場合\_フラグ\_書き込み\_を通じて、セットし、失敗したアプリケーションにします。
-   元の要求がファイルを持たない場合\_フラグ\_書き込み\_を通じて、セットし、アプリケーションに表示成功応答せず、要求が完了しておらず、物理メディアにフラッシュします。
-   「永続的なリソース枯渇」のエラー メッセージを含むシステム イベントが記録されます。
-   エラー コードでは、パーティション マネージャーに戻され、LUN をオフラインにします。

## <a name="span-idstoragespacereclamationusingtheunmapcommandspanspan-idstoragespacereclamationusingtheunmapcommandspanspan-idstoragespacereclamationusingtheunmapcommandspanstorage-space-reclamation-using-the-unmap-command"></a><span id="Storage_Space_Reclamation_Using_the_UNMAP_Command"></span><span id="storage_space_reclamation_using_the_unmap_command"></span><span id="STORAGE_SPACE_RECLAMATION_USING_THE_UNMAP_COMMAND"></span>マッピング解除コマンドを使用してストレージ領域の解放


領域の解放は、ファイルの削除、ファイル システム レベル trim または記憶域の最適化の操作によってトリガーできます。 ファイル システム レベルのトリムは、trim をまたはマッピング解除操作の後に「戻り値 0 の読み取り」を実行するように、記憶域デバイスに対して有効です。

### <a name="span-idspacereclamationoperationinthestoragestackspanspan-idspacereclamationoperationinthestoragestackspanspan-idspacereclamationoperationinthestoragestackspanspace-reclamation-operation-in-the-storage-stack"></a><span id="Space_Reclamation_Operation_in_the_Storage_Stack"></span><span id="space_reclamation_operation_in_the_storage_stack"></span><span id="SPACE_RECLAMATION_OPERATION_IN_THE_STORAGE_STACK"></span>記憶域スタックに領域の解放操作

大きなファイルがファイル システムから削除またはファイル システム レベルのトリムがトリガーされる、Windows Server はファイルの削除またはトリム通知に対応するマッピング解除要求に変換します。 ポートの記憶域ドライバー スタック、SCSI をマップ解除コマンドまたはストレージ デバイスのプロトコルの種類に従って ATA トリム コマンド マッピング解除要求に変換します。 記憶域デバイスの列挙中には、Windows 記憶域スタックは、記憶装置がマッピング解除または TRIM コマンドをサポートするかどうかに関する情報を収集します。 デバイスは、SCSI をマップ解除または ATA のトリミング機能を持つ場合、記憶装置にマッピング解除要求のみが送信されます。 Windows Server には、マップ解除しています Lba、記憶域ターゲット デバイスでの API の実装も提供します。 Windows Server は T10 SCSI WRITE SAME コマンド セットを採用していません。

### <a name="span-idunmaprequestsfromthehyper-vguestoperatingsystemspanspan-idunmaprequestsfromthehyper-vguestoperatingsystemspanspan-idunmaprequestsfromthehyper-vguestoperatingsystemspanunmap-requests-from-the-hyper-v-guest-operating-system"></a><span id="UNMAP_Requests_from_the_Hyper-V_Guest_Operating_System"></span><span id="unmap_requests_from_the_hyper-v_guest_operating_system"></span><span id="UNMAP_REQUESTS_FROM_THE_HYPER-V_GUEST_OPERATING_SYSTEM"></span>HYPER-V ゲスト オペレーティング システムからの要求をマップ解除します。

HYPER-V ホストがかどうかについて照会を送信する仮想マシン (VM) の作成時に仮想ハード_ディスク (VHD) が存在する場所、ストレージ デバイス マッピング解除または TRIM コマンドをサポートしています。 大きなファイルが VM のゲスト オペレーティング システムのファイル システムから削除されると、ゲスト オペレーティング システムは、仮想マシンの仮想ハード_ディスク (VHD) または VHD ファイルにファイルの削除要求を送信します。 VM の VHD または VHD ファイルの次のように、Windows、HYPER-V ホストのクラス ドライバー スタックへの要求、SCSI をマップ解除トンネル。

-   VM に VHD がある場合は、VHD はデータ セットの管理の I/O 制御コード (IOCTL DSM) TRIM 要求に SCSI をマップ解除または ATA のトリミングのコマンドを変換し、ホストの記憶装置に要求を送信します。
-   VM に VHD ファイルがある場合は、VHD のファイル システム SCSI をマップ解除または ATA のトリミングのコマンドをファイル システム レベルのトリムの要求に変換し、ホスト オペレーティング システムに要求を送信します。

Windows HYPER-V には、ゲスト オペレーティング システムからの呼び出しの IOCTL DSM トリムもサポートしています。

### <a name="span-idwindowsoptimizedrivesutilityspanspan-idwindowsoptimizedrivesutilityspanspan-idwindowsoptimizedrivesutilityspanwindows-optimize-drives-utility"></a><span id="Windows_Optimize_Drives_Utility"></span><span id="windows_optimize_drives_utility"></span><span id="WINDOWS_OPTIMIZE_DRIVES_UTILITY"></span>Windows ユーティリティのドライブを最適化します。

エンドユーザーまたはシステム管理者は、手動の要求を作成するか、スケジュールの構成を最適化することによって、領域を再利用するのにドライブの最適化ユーティリティを使用できます。 シン プロビジョニングの LUN をディスク ドライブには、"シン プロビジョニング ドライブ として、ディスク ドライブのメディアの種類が表示されます。

システム管理者は、ドライブの最適化ユーティリティを使用してストレージ領域の統合をスケジュールできます。 ユーティリティは、システム管理者システムに 3 つの連続する失敗した場合は実行をスケジュール設定を通知することもできます。

## <a name="span-idretrievingtheslabmappingstatespanspan-idretrievingtheslabmappingstatespanspan-idretrievingtheslabmappingstatespanretrieving-the-slab-mapping-state"></a><span id="Retrieving_the_Slab_Mapping_State"></span><span id="retrieving_the_slab_mapping_state"></span><span id="RETRIEVING_THE_SLAB_MAPPING_STATE"></span>スラブのマッピングの状態を取得します。


シン プロビジョニング LUN には、すべての論理ブロックはされているスラブ (クラスター) でグループ化されます。 スラブのサイズは、ストレージ デバイスを報告する最適なマップ解除の粒度パラメーターによって設定されます。 すべてスラブは、マップ、割り当て解除または固定の状態に分類されます。 Windows Server では、割り当て解除済みと固定の両方の状態がマップされていない状態として扱われます。 Windows Server では、API の実装、または記憶域の管理操作のシン プロビジョニング Lun から LBA プロビジョニングの状態を取得する、IOCTL DSM 割り当てを提供します。 アプリケーションでは、SCSI コマンドを送信し、特定の範囲内の各スラブのマップまたはマップされていない状態を取得する IOCTL DSM 割り当てルーチンを呼び出すことができます。 プロビジョニングの状態が返される LBA が全体の割り当ての範囲を説明されていない場合、アプリケーションは、残りの LBA 範囲のプロビジョニングの状態を取得するもう 1 つの SCSI コマンドを送信します。

記憶域デバイスは、1 つの戻り LBA 範囲全体を処理する必要はありません。 元の要求部分 LBA 範囲が返された場合、別のコマンドを送信して、残りの LBA 範囲のマッピングの状態を取得します。

 

 




