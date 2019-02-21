---
title: CD-ROM のリアルタイムのストリーミング
description: ストリーミング (または、リアルタイム ストリーミング) は、高速な読み取りおよび書き込み要求を光学式ドライブによって提供される機能です。
ms.assetid: A4093485-076A-4414-A3D2-9285B2AC097B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aef9449c82b5cc3cd18088ab2057539bd57eacd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552965"
---
# <a name="span-idstoragecd-romreal-timestreamingspancd-rom-real-time-streaming"></a><span id="storage.cd-rom_real-time_streaming_"></span>CD-ROM のリアルタイムのストリーミング


ストリーミング (または、リアルタイム ストリーミング) は、高速な読み取りおよび書き込み要求を光学式ドライブによって提供される機能です。 Windows 7 以降の DVD ビデオのストリーミングのサポートは、UDF ファイル システム ドライバー、Udfs.sys、およびビデオ再生のサブシステムを含む、Windows Media Player に Cdrom.sys から、記憶域スタックのすべてのレイヤーで実装されています。

## <a name="span-idaboutreal-timestreamingspanspan-idaboutreal-timestreamingspanspan-idaboutreal-timestreamingspanabout-real-time-streaming"></a><span id="About_real-time_streaming_"></span><span id="about_real-time_streaming_"></span><span id="ABOUT_REAL-TIME_STREAMING_"></span>リアルタイムのストリーミング


一般に、読み取りし、光学式メディアへの書き込みアクセスの特徴は、2 つのプロパティ: 信頼性とパフォーマンスを維持します。 これらのプロパティは、相互に依存 (下位のパフォーマンスは低下信頼性の向上が実現されます) と同時に最大化することはできません。

光学式メディア用のアプリケーションの大部分は信頼性 (つまり、データの整合性) に重点を置いています。 ただし、DVD はレコーダーもデジタル ビデオ camcorders などの特定のアプリケーションでは、持続的なパフォーマンスに重点を置いていて、適切な操作の特定のレベルの保証されたデータのスループットを必要とします。 仕様では、これらのアプリケーションは適切なデータ損失に対する回復力 (たとえば、ビデオ コーデックと仮定するいくつかのフレームが失われることができます)。 これらのアプリケーションでは、信頼性はない値が最も高い優先順位です。 光学式ドライブ (いわゆるリアルタイム ストリーミング) 特別なモードの操作を提供することでこのニーズに対処します。 このモードでのパフォーマンスを向上させる、読み取ったり書き込んだりするエラーは無視され、再試行またはエラーの修正または防止にドライブが実行されません。

## <a name="span-iddevelopersupportforreal-timestreaminginwindowsspanspan-iddevelopersupportforreal-timestreaminginwindowsspanspan-iddevelopersupportforreal-timestreaminginwindowsspandeveloper-support-for-real-time-streaming-in-windows"></a><span id="Developer_support_for_real-time_streaming_in_Windows"></span><span id="developer_support_for_real-time_streaming_in_windows"></span><span id="DEVELOPER_SUPPORT_FOR_REAL-TIME_STREAMING_IN_WINDOWS"></span>Windows では、リアルタイム ストリーミングに対する開発者のサポート


以降、CD-ROM クラス ドライバー、Windows 7 では、Cdrom.sys、ストリーミングの低レベルの読み取りをサポートしているし、書き込み要求 (MMC 仕様の/WRITE12 READ12 コマンド)。 ユーザー モード アプリケーションで使用できます、 [ **IOCTL\_CDROM\_を有効にする\_ストリーミング**](https://msdn.microsoft.com/library/windows/hardware/gg441241)を有効にするか、生データを読み取るのストリーミングを無効にすると書き込みの I/O 制御コード (IOCTL)要求します。 これらの読み取りおよび書き込み要求は、生の CD または DVD-ROM デバイス用に開かれたハンドルを使用して実行されます。

さらに、カーネル モードのコンポーネントの変更があるように Cdrom.sys ハンドル[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)要求。 クラスのドライバーでは、リアルタイム ストリーミング要求が、デバイスの機能を満たすことを検証します。 この機能を実装するために Windows 7 に導入ストリーミング フラグを**SL\_リアルタイム\_ストリーム**、ドライバーの[ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659). このフラグはストリーミングのすべての読み取りのアサートまたは書き込みを要求し、ストリーミング以外のすべての要求がクリアします。

記憶域ドライバー スタックでこれらの変更は、リアルタイムのデータを含むファイルに対して保証された速度で読み取り/書き込み操作を実行する (特に、ファイル システム ドライバーおよびアプリケーション) で上位のレイヤーを許可します。 Windows 7 以降を使用してリアルタイム ストリーミング用のファイルをマークすることができます、 [ **FSCTL\_マーク\_処理**](https://msdn.microsoft.com/library/windows/desktop/aa364576)制御コードとを設定して、ストリーミングのモードを指定します。**マーク\_処理\_リアルタイム**フラグ、 [**マーク\_処理\_情報**](https://msdn.microsoft.com/library/windows/desktop/aa365229)構造体。

図 1 は、正規表現とストリーミングの読み取りと書き込み要求と UDF ファイル システムと CDROM クラス ドライバー間のリレーションシップを示しています。

![図 1: リアルタイム ストリーミング cdrom.sys および udfs.sys でのサポート](images/cdromstreaming.png)

DVD の再生アプリケーションとファイル システム ドライバー Cdrom.sys (最下位レベル) の生のストリーミング サポートにアクセスする Ioctl を使用して、ストリーミング Udfs.sys で導入されたモードのファイル システムのサポートを使用してまたはの選択肢があります。 アプリケーションでは、Windows のビデオの再生をサブ システム全体としても指定できます。 再生、に加えて、Cdrom.sys とファイル システム レイヤーは、ストリーミングの記録をサポートします。

## <a name="span-idverifyingdevicesupportforreal-timestreamingusingioctlsspanspan-idverifyingdevicesupportforreal-timestreamingusingioctlsspanspan-idverifyingdevicesupportforreal-timestreamingusingioctlsspanverifying-device-support-for-real-time-streaming-using-ioctls"></a><span id="Verifying_device_support_for_real-time_streaming_using_IOCTLs"></span><span id="verifying_device_support_for_real-time_streaming_using_ioctls"></span><span id="VERIFYING_DEVICE_SUPPORT_FOR_REAL-TIME_STREAMING_USING_IOCTLS"></span>デバイスでのサポートを確認しています Ioctl を使用したリアルタイム ストリーミング。


-   使用[ **IOCTL\_CDROM\_取得\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff559334)ストリーミング機能が存在し、現在を判断します。

## <a name="span-idenablingordisablingreal-timestreamingusingioctlsspanspan-idenablingordisablingreal-timestreamingusingioctlsspanspan-idenablingordisablingreal-timestreamingusingioctlsspanenabling-or-disabling-real-time-streaming-using-ioctls"></a><span id="Enabling_or_disabling_real-time_streaming_using_IOCTLs"></span><span id="enabling_or_disabling_real-time_streaming_using_ioctls"></span><span id="ENABLING_OR_DISABLING_REAL-TIME_STREAMING_USING_IOCTLS"></span>有効化または Ioctl を使用したリアルタイム ストリーミングを無効にします。


-   使用して、 [ **IOCTL\_CDROM\_を有効にする\_ストリーミング**](https://msdn.microsoft.com/library/windows/hardware/gg441241)を有効にし、生データを読み取るのストリーミングのモードを無効にする、または書き込み要求の I/O 制御コード。 この IOCTL パラメーターは出力がないと、サポート、 [ **CDROM\_ストリーミング\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/gg441238)入力パラメーターとして構造体。

    この IOCTL では、有効または、ハンドルごとにストリーミングのモードを無効にします。 既定では、ストリーミングはすべて新しく開かれた生の cd-rom ドライブ ハンドルを無効になります。 ファイル システムを使用しないし、生データを業務に対応する再生アプリケーションは、同じデバイスの 2 つのファイル ハンドルを開く必要があります。 ファイル システムのメタデータとファイルのリアルタイムのストリーミングの 1 つの正規表現の 1 つ。

## <a name="span-idspecifyingreal-timestreamingforirpmjreadandirpmjwriterequestsspanspan-idspecifyingreal-timestreamingforirpmjreadandirpmjwriterequestsspanspan-idspecifyingreal-timestreamingforirpmjreadandirpmjwriterequestsspanspecifying-real-time-streaming-for-irpmjread-and-irpmjwrite-requests"></a><span id="Specifying_real-time_streaming_for_IRP_MJ_READ_and_IRP_MJ_WRITE_requests"></span><span id="specifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requests"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_IRP_MJ_READ_AND_IRP_MJ_WRITE_REQUESTS"></span>IRP のリアルタイム ストリーミングを指定する\_MJ\_読み取りおよび IRP\_MJ\_書き込み要求


-   SL\_リアルタイム\_ストリーム フラグ、 [ **IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)(Irp)-&gt;Flags フィールド コントロールの読み取りし、書き込みストリーミング要求 ([ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff549327)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff549427))。 フラグが読み取りすべてのストリーミングに設定されてと書き込みを要求し、ストリーミング以外のすべての要求をクリアします。 場合、SL\_リアルタイム\_ストリーム フラグが設定されて、Cdrom.sys READ10 または WRITE10 SCSI コマンドではなく READ12 および WRITE12 SCSI コマンドを使用して、ストリーミングの要求を実行します。 場合、SL\_リアルタイム\_、IRP のストリームのフラグが設定されて、デバイスが挿入された現在のメディアのストリーミングをサポートしていませんが、IRP はステータス コードの状態で拒否されます\_無効な\_デバイス\_を要求します。

## <a name="span-idspecifyingreal-timestreamingforafileusingfsctlsspanspan-idspecifyingreal-timestreamingforafileusingfsctlsspanspan-idspecifyingreal-timestreamingforafileusingfsctlsspanspecifying-real-time-streaming-for-a-file-using-fsctls"></a><span id="Specifying_real-time_streaming_for_a_file_using_FSCTLs"></span><span id="specifying_real-time_streaming_for_a_file_using_fsctls"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_A_FILE_USING_FSCTLS"></span>リアルタイムのストリーミング FSCTLs を使用してファイルを指定します。


-   ファイルの種類に関係なく、リアルタイムの読み取りの動作のすべてのファイルをマークすることができます。 これを行うには、次のように設定します、**マーク\_処理\_リアルタイム**フラグ、 [**マーク\_処理\_情報**](https://msdn.microsoft.com/library/windows/desktop/aa365229)構造、および。送信し、 [ **FSCTL\_マーク\_処理**](https://msdn.microsoft.com/library/windows/desktop/aa364576)コードを制御します。 バッファなし I/O には、このフラグでマークされたファイルを開く必要があります。
-   アプリケーションがリアルタイム動作は、以前フラグが設定されたファイルをマーク解除を設定して、**マーク\_処理\_いない\_リアルタイム**フラグでマーク\_ハンドル\_情報構造体。
-   場合 FSCTL\_マーク\_マークが付いたハンドル制御コードが送信される\_処理\_リアルタイムと、CD や DVD ドライブまたはメディアがリアルタイムのストリーム配信機能はサポートされていません、IOCTLの状態を取得することを示す\_無効な\_デバイス\_を要求します。 状態のバッファリングせずにハンドルが開かれたかどうか\_無効な\_デバイス\_も要求が返されます。

## <a name="span-idperformingoptimumpowercalibrationopcbeforewritingspanspan-idperformingoptimumpowercalibrationopcbeforewritingspanspan-idperformingoptimumpowercalibrationopcbeforewritingspanperforming-optimum-power-calibration-opc-before-writing"></a><span id="Performing_Optimum_Power_Calibration__OPC__before_writing"></span><span id="performing_optimum_power_calibration__opc__before_writing"></span><span id="PERFORMING_OPTIMUM_POWER_CALIBRATION__OPC__BEFORE_WRITING"></span>書き込みの前に最適な電源の調整 (OPC) を実行します。


一部のアプリケーションは、ストリーミングの最初の書き込みが完了するには、OPC を待機する必要があるないように、事前に OPC 手順を実行する可能性があります。 Cdrom.sys と呼ばれる IOCTL を提供するのには、 [ **IOCTL\_CDROM\_送信\_OPC\_情報**](https://msdn.microsoft.com/library/windows/hardware/gg441243)します。

## <a name="span-iddeterminingthereadwritespeedforthedrivespanspan-iddeterminingthereadwritespeedforthedrivespanspan-iddeterminingthereadwritespeedforthedrivespandetermining-the-readwrite-speed-for-the-drive"></a><span id="Determining_the_read_write_speed_for_the_drive"></span><span id="determining_the_read_write_speed_for_the_drive"></span><span id="DETERMINING_THE_READ_WRITE_SPEED_FOR_THE_DRIVE"></span>ドライブの読み取り/書き込み速度を決定します。


MMC の仕様は、アプリケーションが望ましい読み取りを示すことと、ドライブが優れたバランスを検索できるように、I/O のストリーミングを使用する前に、書き込み速度、読み取りし、書き込みの品質のスループットをお勧めします。 アプリケーションで使用できます、 [ **IOCTL\_CDROM\_設定\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff559381)を優先の速度を示します。 ドライブのサポートされる機能を確認するのには、Windows 7 が導入された、 [ **IOCTL\_CDROM\_取得\_パフォーマンス**](https://msdn.microsoft.com/library/windows/hardware/gg441242)として受け取り、コードの制御、入力、 [ **CDROM\_パフォーマンス\_要求**](https://msdn.microsoft.com/library/windows/hardware/gg441233)構造体。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[**IOCTL\_CDROM\_ENABLE\_STREAMING**](https://msdn.microsoft.com/library/windows/hardware/gg441241)  
[**IOCTL\_CDROM\_GET\_PERFORMANCE**](https://msdn.microsoft.com/library/windows/hardware/gg441242)  
[**IOCTL\_CDROM\_SEND\_OPC\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/gg441243)  
[**IOCTL\_CDROM\_SET\_SPEED**](https://msdn.microsoft.com/library/windows/hardware/ff559381)  
[**FSCTL\_マーク\_処理**](https://msdn.microsoft.com/library/windows/desktop/aa364576)  
[**マーク\_処理\_情報**](https://msdn.microsoft.com/library/windows/desktop/aa365229)  
[**CDROM\_パフォーマンス\_要求**](https://msdn.microsoft.com/library/windows/hardware/gg441233)  



