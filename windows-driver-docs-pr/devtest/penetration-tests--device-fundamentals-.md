---
title: 侵入テスト (Device Fundamental)
description: デバイスの基本侵入テストは、セキュリティテストの重要なコンポーネントであるさまざまな形式の入力攻撃を実行します。 攻撃および侵入テストは、ソフトウェアインターフェイスの脆弱性を特定するのに役立ちます。
ms.assetid: 53EBAF4B-2CEF-492B-98B8-DA199FDFBC46
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8e15f035e63d8700e5c8b39d2c9f2a70277f714
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839334"
---
# <a name="penetration-tests-device-fundamentals"></a>侵入テスト (Device Fundamental)


デバイスの基本侵入テストは、セキュリティテストの重要なコンポーネントであるさまざまな形式の入力攻撃を実行します。 攻撃および侵入テストは、ソフトウェアインターフェイスの脆弱性を特定するのに役立ちます。

## <a name="penetration"></a>貫


侵入テストには、ファジーテストと i/o [Spy](iospy.md)および[i/o 攻撃](ioattack.md)テストという2つのカテゴリのテストが含まれています。 ファジーテストは、**デバイスパス Exceriser**テストツールの機能でもありました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テスト</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>I/o Spy を無効にする</p></td>
<td align="left"><p>1つ以上のデバイスで<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/o Spy</a>を無効にします。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOSpy_DisableSupport</p>
<p><strong>テストメソッド:</strong>DisableIoSpy</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="display_i_o_spy-enabled_device"></span>I/o Spy 対応デバイスを表示する</p></td>
<td align="left"><p><a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/o Spy</a>が有効になっているデバイスを表示します。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOSpy_DisplayEnabledDevices</p>
<p><strong>テストメソッド:</strong>DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>I/o Spy を有効にする</p></td>
<td align="left"><p>1つまたは複数のデバイスで<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/o Spy</a>を有効にします。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOSpy_EnableSupport</p>
<p><strong>テストメソッド:</strong>EnableIoSpy</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>DFD</em> - iospy データファイルへのパスを指定します。 既定の場所は%SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_misc_api_test"></span>ファジーのその他の API テスト</p></td>
<td align="left"><p>ファジーのその他の API テストは、ドライバーがカーネルモードドライバーからのさまざまな一般的な呼び出しを処理できるかどうかを判断するテストです。</p>
<p>テストには、次のテストが含まれています。</p>
<ul>
<li><p>有効なデータバッファーポインター、さまざまな長さ (ゼロを含む)、および0、-1、64ビットのオフセットを含むさまざまなバイトオフセットを指定して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)"><strong>Zwreadfile</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)"><strong>zwreadfile</strong></a>を呼び出します。</p></li>
<li><p>を呼び出して、I/0 をキャンセルし、バッファーをフラッシュします。</p></li>
<li><p>一連のディレクトリクエリは、有効なユーザーデータバッファーポインターとさまざまなバッファー長 (ゼロを含む) を持つ共通ファイル情報クラスを使用して呼び出します。</p></li>
<li><p>ディレクトリクエリは、仮想 DOS コンピューター (VDM) の制御下で実行されているプログラムによって発行されたものと同様の呼び出しを行います。</p></li>
<li><p>を呼び出して、さまざまなバッファーサイズと長さを持つファイルの拡張属性を取得します。</p></li>
<li><p>を呼び出して、セクションオブジェクトを作成して閉じます。さまざまなセクションのページ保護とセクション割り当て属性 (コミット済みセクション、イメージファイルセクション) を使用します。</p></li>
<li><p>を呼び出して、ファイルをロックおよびロック解除します。</p></li>
<li><p>を呼び出して、ボリュームのクォータエントリを取得します。</p></li>
<li><p>ファイル属性テスト。 <strong>objectattributes</strong>構造体への有効なポインターを持つ一連のファイル属性クエリ。</p>
<p>ファイル属性のテストには、省略可能なゼロの長さのテストがあります。 ファジーテストでは、ファイルの拡張属性を取得するときに、空の (長さゼロの) クエリと無効なバッファーアドレスをドライバーに渡します。</p></li>
</ul>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoMiscAPITest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Misc_API_with_zero-length_query_test"></span><span id="fuzz_misc_api_with_zero-length_query_test"></span><span id="FUZZ_MISC_API_WITH_ZERO-LENGTH_QUERY_TEST"></span>長さゼロのクエリテストを使用したファジーのその他の API</p></td>
<td align="left"><p>このテストは、ファジーのその他の API テストと同じテストを実行します。この時間が経過すると、ファイルの拡張属性を取得しようとしているときに、空の (長さゼロの) クエリと無効なバッファーアドレスがドライバーに渡されます。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoMiscAPIWithZeroLengthTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_open_and_close_test"></span>ファジーオープンおよび終了テスト</p></td>
<td align="left"><p>このテストでは、多数の作成オープンクローズシーケンスが実行します。</p>
<p>このテストの詳細については、「<a href="#about-the-fuzz-open-and-close-test" data-raw-source="[About the Fuzz open and close test](#about-the-fuzz-open-and-close-test)">ファジーオープンと終了テストについ</a>て」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoOpenCloseTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Query_and_Set_File_Information_test_"></span><span id="fuzz_query_and_set_file_information_test_"></span><span id="FUZZ_QUERY_AND_SET_FILE_INFORMATION_TEST_"></span>ファジークエリとファイル情報の設定のテスト</p></td>
<td align="left"><p>このテストでは、デバイスのオブジェクト、ファイル、およびボリュームの情報を取得して変更するための呼び出しが発行されます。</p>
<p><em>クエリとファイル情報の設定のテスト</em>中に、ファジーテストの問題によって、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本的なオープン操作</a>やその他のオープン操作 (操作を含む) によって開かれたデバイスのオブジェクト、ファイル、およびボリュームの情報を取得および変更するためにが呼び出されます。ファジーサブオープンテストによって実行されます。</p>
<p>ファジーテストでは、有効なバッファーとさまざまなバッファー長とファイル情報クラスを使用して、各クエリまたは set 呼び出しが少なくとも1024回発行されます。 また、各種類の要求は、無効なバッファーポインターとゼロバッファー長を使用して送信されます。</p>
<p>保護オプションを設定する<em>Changebufferprotectionflags</em>パラメーターを使用する場合、ファジーテストでは、各クエリおよび set 呼び出しのバッファーのセキュリティ設定が異なります。</p>
<p>このテストでは、ファジーサブオープンテストも実行されます。</p>
<p>このテストでは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)"><strong>、Zwqueryinformationfile</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)"><strong>zwqueryinformationfile</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567070" data-raw-source="[&lt;strong&gt;ZwQueryVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567070)"><strong>zwqueryvolumeinformationfile</strong></a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff567112" data-raw-source="[&lt;strong&gt;ZwSetVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567112)"><strong>zwsetvolumeinformationfile</strong></a>関数を使用します。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoQueryAndSetFileInformationTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Query_and_Set_Security_test"></span><span id="fuzz_query_and_set_security_test"></span><span id="FUZZ_QUERY_AND_SET_SECURITY_TEST"></span>ファジークエリとセキュリティテストの設定</p></td>
<td align="left"><p>このテストは、の呼び出しを発行して、セキュリティ記述子を取得し、デバイスのセキュリティの状態を変更します。</p>
<p><em>クエリとセキュリティテスト</em>の実行中、ファジーテストはを呼び出して、セキュリティ記述子を取得し、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本的なオープン操作</a>およびその他のオープン操作によって開かれたデバイスのセキュリティ状態を変更します。これには、によって実行される操作も含まれます。ファジーサブオープンテスト。</p>
<p>ファジーテストでは、有効なバッファーとさまざまなバッファー長とセキュリティ情報の種類 (OWNER_SECURITY_INFORMATION、GROUP_SECURITY_INFORMATION、DACL_SECURITY_INFORMATION、SACL_SECURITY_) を使用して、各クエリまたは設定呼び出しを少なくとも1024回発行します。情報の種類はありません)。 また、各種類の要求は、無効なバッファーポインターとゼロバッファー長を使用して送信されます。</p>
<p>保護オプションを設定する<em>Changebufferprotectionflags</em>パラメーターを使用する場合、ファジーテストでは、各クエリおよび set 呼び出しのバッファーのセキュリティ設定が異なります。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoQueryAndSetSecurityTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Random_FSCTL_test___Fuzz_Random_IOCTL_test_"></span><span id="fuzz_random_fsctl_test___fuzz_random_ioctl_test_"></span><span id="FUZZ_RANDOM_FSCTL_TEST___FUZZ_RANDOM_IOCTL_TEST_"></span>ファジーランダム FSCTL テスト/ファジーランダム IOCTL テスト</p></td>
<td align="left"><p>このテストでは、関数コード、デバイスの種類、データ転送方法、および指定された範囲の値からランダムに選択されたアクセス要件を使用して、DeviceIoControl 関数に対する一連の呼び出しを発行します。 呼び出しには、有効かつ無効なバッファーポインターと長さを持つ入力バッファーと出力バッファー、およびランダムに生成されたコンテンツが含まれます。</p>
<p>ランダムテスト中、ファジーテストでは、関数コード、デバイスの種類、データ転送方法、および指定された範囲の値からランダムに選択されるアクセス要件を使用して、 <strong>DeviceIoControl</strong>関数に対する一連の呼び出しを発行します。 呼び出しには、有効かつ無効なバッファーポインターと長さを持つ入力バッファーと出力バッファー、およびランダムに生成されたコンテンツが含まれます。</p>
<p>このファジーテストでは、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本的なオープン操作</a>と追加の開いているテスト中に開かれたすべてのデバイスに対してランダムテストを実行します。 このテストは、次のパラメーターを使用してカスタマイズできます。</p>
<ul>
<li><p><em>Minfunctioncode</em>と<em>maxfunctioncode</em>を使用して、呼び出しで使用される IOCTL または FSCTL 関数コードの範囲を指定します。</p></li>
<li><p><em>MinDeviceType</em>と<em>MaxDeviceType</em>を使用して、呼び出しで使用されるデバイスの種類の範囲を指定します。</p></li>
<li><p><em>SeedNumber</em>を使用して、乱数生成ルーチンのシード番号を指定します。</p></li>
</ul>
<p>ファジーテストで乱数を生成するために使用される関数は、乱数を生成するアルゴリズムの開始番号である<em>シード番号</em>を使用します。 テスト条件を再現するには、 <em>seed number</em>パラメーターを使用して、元のテスト評価で使用されたシード番号を指定します。</p>
<p>ランダムテストの一部として、調整された<em>ランダムテスト</em>が含まれます。 調整されたランダムテストでは、ランダムテストの結果を使用して、IOCTL または FSCTL 要求へのドライバーの応答を詳細に調べます。 調整されたランダムテストは、ランダムなテストが行われなかった領域と、ランダムなテスト呼び出しによって返された状態に基づいて、予想どおりに応答しなかったドライバーをプローブします。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoRandomIOCTLTest, DoRandomFSCTLTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>MinInBuffer</em></p>
<p><em>MaxInBuffer</em></p>
<p><em>MinOutBuffer</em></p>
<p><em>MaxOutBuffer</em></p>
<p><em>MaxRandomCalls</em></p>
<p><em>MaxTailoredCalls</em></p>
<p><em>SeedNumber</em></p>
<p><em>MinDeviceType</em></p>
<p><em>MaxDeviceType</em></p>
<p><em>MinFunctionCode</em></p>
<p><em>MaxFunctionCode</em></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_sub-opens_test"></span>ファジーサブオープンテスト</p></td>
<td align="left"><p>テストでは、デバイスの名前空間でオブジェクトを開くために、高速な一連の呼び出しが実行されます。 これらの呼び出しでは、デバイスで始まるパスが渡され、長さとコンテンツが異なる任意の名前と文字列が含まれます。</p>
<p><em>相対オープンテスト</em>(<em>サブオープンテスト</em>とも呼ばれます) の間に、ファジーテストはデバイスの<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access" data-raw-source="[namespace](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)">名前空間</a>内のオブジェクトを開こうとします。</p>
<p>このテスト中、ファジーテストは、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本的なオープン操作</a>やその他のオープン操作を使用して開かれたデバイスの名前空間でオブジェクトを開くための、迅速な一連の呼び出しを実行します。 このような呼び出しでは、デバイスで始まるパスが使用され、長さとコンテンツが異なる任意の名前と文字列が含まれます。</p>
<p>このテストでは、ドライバーまたはファイルシステムが、名前空間内の開いている要求をどのように管理するかを決定します。 特に、ドライバーが名前空間内のオープン要求をサポートしていない場合、要求に失敗するか、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)"><strong>を使用するときに FILE_DEVICE_SECURE_OPEN デバイスの特性を設定することによって、承認されていないアクセスを防ぐ必要があります。デバイスオブジェクトを作成</strong></a>します。</p>
<p>デバイスの名前空間の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access" data-raw-source="[Controlling Device Namespace Access](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)">デバイスの名前空間へのアクセスの制御</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoSubOpensTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Sub-opens_with_Streams_test"></span><span id="fuzz_sub-opens_with_streams_test"></span><span id="FUZZ_SUB-OPENS_WITH_STREAMS_TEST"></span>ストリームテストでのファジーサブオープン</p></td>
<td align="left"><p>このテストでは、デバイス上のさまざまな名前付きデータストリームを開こうとします。 このテストでは、コンテンツと文字を含む一連の任意のストリーム名を使用します。これは、一部のデバイスで他の用途に有効である可能性があります。</p>
<p><em>ストリームテスト</em>中、ファジーテストはデバイス上のさまざまな名前付きデータストリームを開こうとします。 テストでは、コンテンツと文字を含む一連の任意のストリーム名を使用します。これは、一部のデバイスで他の用途に有効である可能性があります。 このテストでは、ドライバーがデータストリーム要求を適切に処理できるかどうかを判断します。特に、ドライバーがデータストリームをサポートしていないデバイスをエクスポートする場合は、</p>
<p><em>名前付きデータストリーム</em>は、ファイルオブジェクトの属性です。 名前付きデータストリームを指定するには、ファイルの名前、コロン、およびデータストリームの名前を記述します。たとえば、 <em>accessdate</em>は、名前付きのデータストリーム、つまり File01 ファイルの属性に記述されているとします。</p>
<p>ファジーテストでは、テストで使用されているストリーム名を記録します。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoSubOpensWithStreamsTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Zero-Length_Buffer_FSCTL_test___Fuzz_Zero-Length_Buffer_IOCTL_test"></span><span id="fuzz_zero-length_buffer_fsctl_test___fuzz_zero-length_buffer_ioctl_test"></span><span id="FUZZ_ZERO-LENGTH_BUFFER_FSCTL_TEST___FUZZ_ZERO-LENGTH_BUFFER_IOCTL_TEST"></span>ファジーゼロ長バッファー FSCTL テスト/ファジーゼロ長バッファー IOCTL テスト</p></td>
<td align="left"><p>このテストでは、入力バッファーまたは出力バッファーの長さが0の<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl 関数</strong></a>の一連の呼び出しが発行されます。 このテストでは、さまざまな関数コード、デバイスの種類、データ転送方法、およびアクセス要件を使用して、さまざまなファイルシステム制御コードを生成します。</p>
<p>長さ0のバッファーテスト中、ファジーテストでは、入力バッファーまたは出力バッファーの長さが0の<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl 関数</strong></a>に対する一連の呼び出しが発行されます。 テストでは、さまざまな関数コード、デバイスの種類、データ転送方法、およびアクセス要件を使用して、さまざまな i/o 制御コードが生成されます。 I/o 制御コードの内容については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes" data-raw-source="[Defining I/O Control Codes](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)">I/o 制御コードの定義</a>」を参照してください。</p>
<p>無効なバッファーポインターのドライバーの処理をテストするために、これらのユーザーモード呼び出しのバッファーポインターは、(0xFFFFFC00 などの) カーネル仮想アドレス空間に高いアドレスを指定します。</p>
<p>ファジーテストでは、基本および追加の開いているテスト中に開かれたすべてのデバイスで、ゼロ長のバッファーテストを実行します。 このテストをカスタマイズするには、 <em>Minfunctioncode</em>および<em>maxfunctioncode</em>コマンドパラメーターを使用して、呼び出しで使用される IOCTL または FSCTL 関数コードの範囲を指定します。また、 <em>MinDeviceType</em>と<em>MaxDeviceType</em>を指定するには、呼び出しで使用されるデバイスの種類の範囲。</p>
<p><strong>テストバイナリ:</strong>Devfund_DevicePathExerciser</p>
<p><strong>テストメソッド:</strong>DoZeroLengthBufferIOCTLTest, DoZeroLengthBufferFSCTLTest</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>MinDeviceType</em></p>
<p><em>MaxDeviceType</em></p>
<p><em>MinFunctionCode</em></p>
<p><em>MaxFunctionCode</em></p>
<p><em>DoPoolCheck</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>装う</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Run_I_O_Attack"></span><span id="run_i_o_attack"></span><span id="RUN_I_O_ATTACK"></span>I/o 攻撃の実行</p></td>
<td align="left"><p>指定されたデバイスまたはデバイスで i/o<a href="ioattack.md" data-raw-source="[I/O Attack](ioattack.md)">攻撃</a>を実行します。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOAttack_DeleteDataFile</p>
<p><strong>テストメソッド:</strong>RunIoAttack</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-fuzz-open-and-close-test"></a>ファジーのオープンテストと終了テストについて


ファジーオープンおよびクローズテストでは、指定されたデバイスまたはデバイスのインスタンスを開いたり閉じたりするためのさまざまな方法が採用されています。これには、[基本的なオープン操作](#basic-open-operations)、[デバイスの直接開い](#direct-device-open-operations)ている操作、および開閉[テスト](#open-and-close-test)があります。

### <a name="basic-open-operations"></a>基本的なオープン操作

*基本的なオープン操作*中、ファジーテストは、指定されたデバイスまたは指定されたドライバーによってエクスポートされたデバイスのインスタンスを、さまざまな方法とオプションを使用して繰り返し開きます (作成します)。

ファジーテストでは、常に基本的なオープン操作が実行されます。 これらを選択する必要はなく、テストセッションから除外することもできません。

このファジーテストでは、デバイスに適したシステムサービス ([Zwxxx ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567122(v=vs.85))) を呼び出すことにより、すべてのオープン操作をユーザーモードで実行します。 開いている呼び出しによってデバイスへのハンドルが返された場合、ファジーテストではハンドルを使用して、テストセッション用に選択した他のデバイステストを実行します。

基本的なオープン操作には、次の5種類があります。

-   **Standard オープン。** ファジーテストでは、デバイスを非同期に開き、ネイティブデバイス名のみを指定します。

-   **バックスラッシュを追加して開きます。** このファジーテストでは、デバイス名に対して開いている呼び出しの後に、デバイス内のルートディレクトリを開こうとしているかのように、\\デバイス\\cdrom\\などの円記号 (\)など) が発行されます。

    この操作では、ドライバーまたはファイルシステムが、名前空間内の開いている要求をどのように管理するかを決定します。 特に、デバイスが名前空間内のオープン要求をサポートしていない場合、ドライバーは、要求を失敗させるか、ファイル\_デバイス\_設定することによって、\_開いているデバイスの特性を呼び出し時に保護する必要があります。デバイスオブジェクトを作成するための[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)または[**iocreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 。

-   **名前付きパイプとして開きます。** このファジーテストでは、デバイスを開き、デバイスへの名前付きパイプを確立します。 アクセスパラメーター (読み取りアクセス) は、最初は読み取りと書き込みに設定されますが、要求が失敗した場合は調整されます。 デバイスが名前付きパイプをサポートしていない場合、要求は失敗します。

-   **をメールスロットとして開きます。** このファジーテストでは、デバイスをメールスロットとして開きます。 デバイスがこの種類の接続をサポートしていない場合、要求は失敗します。

-   **をツリー接続として開きます。** このファジーテストでは、リモートネットワークアクセスで使用するツリー接続としてデバイスを開きます。 アクセスパラメーター (読み取りアクセス) は、最初は読み取りと書き込みに設定されますが、要求が失敗した場合は調整されます。 デバイスがこの種類の接続をサポートしていない場合、要求は失敗します。

開いている呼び出しで使用されるパラメーターは、デバイスの特性に応じて異なり、呼び出しが成功する可能性があります。 たとえば、呼び出しがデバイスのセキュリティ要件を満たしていなかったために基本的なオープン操作が失敗した場合、ファジーテストでは、アクセスの少ない要求で開いている操作を繰り返します。 たとえば、書き込みアクセスを要求したオープン操作によってセキュリティ違反エラーが返された場合、open は読み取りアクセスの要求と共に繰り返されます。

### <a name="direct-device-open-operations"></a>デバイスが開いている直接の操作

デバイスの*直接オープン操作*中、ファジーテストでは、ファイルシステム内のファイルとしてではなく、デバイスとしてデバイスを直接開きます。 デバイスの直接開いている操作は常に同期されます。 呼び出しが成功した場合、ファジーテストでは、指定されたハンドルを使用して、選択した他のテストを実行します。

### <a name="open-and-close-test"></a>テストを開いて閉じる

*オープンテストと終了テスト*中、ファジーテストでは複数のスレッドが作成されます。それぞれのスレッドで、多数の作成オープンクローズシーケンスが実行されます。 これは、それ以外の単純な呼び出しや予想される呼び出しの大量の処理をドライバーがどのように処理するかをテストします。

オープンおよびクローズテストでは、[基本的なオープン操作](#basic-open-operations)で使用されているのと同じオプションを使用して、追加の円記号テストを開き、これらのテストの直前に実行します。

## <a name="related-topics"></a>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

[デバイスの基本テストを選択して構成する方法](https://docs.microsoft.com/windows-hardware/drivers)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://docs.microsoft.com/windows-hardware/drivers)

[提供されている WDTF シンプル I/O プラグイン](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

 

 






