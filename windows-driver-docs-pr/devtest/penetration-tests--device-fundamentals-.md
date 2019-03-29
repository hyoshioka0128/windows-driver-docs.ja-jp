---
title: 侵入テスト (Device Fundamental)
description: デバイスの基礎の侵入テストは、セキュリティのテストの重要なコンポーネントである入力による攻撃のさまざまなフォームを実行します。 攻撃および侵入テストは、ソフトウェア インターフェイスでの脆弱性を識別に役立つことができます。
ms.assetid: 53EBAF4B-2CEF-492B-98B8-DA199FDFBC46
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4326689b9b276cc1f7be8d753042b52dd15f6d64
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464091"
---
# <a name="penetration-tests-device-fundamentals"></a>侵入テスト (Device Fundamental)


デバイスの基礎の侵入テストは、セキュリティのテストの重要なコンポーネントである入力による攻撃のさまざまなフォームを実行します。 攻撃および侵入テストは、ソフトウェア インターフェイスでの脆弱性を識別に役立つことができます。

## <a name="penetration"></a>侵入


侵入テストでは、テストの 2 つのカテゴリがあります。ファジー テストと[I/O スパイ](iospy.md)と[I/O 攻撃](ioattack.md)テストします。 ファジー テストされたの機能でも、**デバイス パス Exceriser**テスト ツールです。

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
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>I/O スパイを無効にします。</p></td>
<td align="left"><p>無効にする<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/O スパイ</a>1 つ以上のデバイスでします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOSpy_DisableSupport.wsc</p>
<p><strong>メソッドをテストします。</strong>DisableIoSpy</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="display_i_o_spy-enabled_device"></span>I/O Spy が有効なデバイスを表示します。</p></td>
<td align="left"><p>デバイスを表示する<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/O スパイ</a>有効にします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOSpy_DisplayEnabledDevices.wsc</p>
<p><strong>メソッドをテストします。</strong>DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>I/O スパイを有効にします。</p></td>
<td align="left"><p>有効にする<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/O スパイ</a>1 つまたは複数のデバイスにします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOSpy_EnableSupport.wsc</p>
<p><strong>メソッドをテストします。</strong>EnableIoSpy</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>DFD</em> - IoSpy データ ファイルへのパスを指定します。 既定の場所は %SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_misc_api_test"></span>ファジー テストの他の API</p></td>
<td align="left"><p>その他の API をファジー テストは、ドライバーが、さまざまなカーネル モード ドライバーからの一般的な呼び出しを処理できるかどうかを決定するテストです。</p>
<p>テストには、次のテストが含まれています。</p>
<ul>
<li><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff567072" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567072)"> <strong>ZwReadFile</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff567121" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567121)"> <strong>ZwWriteFile</strong></a>、有効なデータ バッファーのポインターを指定する、(0 を含む) の長さを可変とバイト オフセットには、0、-1 を含むさまざまなと 64 ビットのバイト オフセット。</p></li>
<li><p>取り消しは呼び出し/0 バッファーをフラッシュします。</p></li>
<li><p>一連のディレクトリのクエリでは、有効なユーザー データのバッファー ポインターを一般的なファイル情報クラスを使用し、バッファー長が (0 を含む) をさまざまなを呼び出します。</p></li>
<li><p>ディレクトリのクエリを呼び出すコントロール仮想 DOS コンピューター (VDM) の下で実行されているプログラムによって発行されたものと似ています。</p></li>
<li><p>さまざまなバッファー サイズと長さを持つファイルの拡張属性を取得するために呼び出します。</p></li>
<li><p>呼び出しを作成し、セクション ページ保護との 2 次元断面属性の割り当て (コミットのセクションで、イメージ ファイルのセクション) をさまざまなセクションのオブジェクトを閉じます。</p></li>
<li><p>ロックおよびファイルをロック解除を呼び出します。</p></li>
<li><p>ボリュームのクォータ エントリを取得するために呼び出します。</p></li>
<li><p>ファイル属性のテスト、一連のファイル属性のクエリに対する有効なポインターで、 <strong>ObjectAttributes</strong>構造体。</p>
<p>ファイル属性のテストには、必要に応じて、長さ 0 のテストがあります。 ファイルの拡張属性を取得中には、ファジー テストは、ドライバーに、空 (長さが 0) のクエリと、無効なバッファーのアドレスを渡します。</p></li>
</ul>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoMiscAPITest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Misc_API_with_zero-length_query_test"></span><span id="fuzz_misc_api_with_zero-length_query_test"></span><span id="FUZZ_MISC_API_WITH_ZERO-LENGTH_QUERY_TEST"></span>長さ 0 のクエリのテストを使用したその他の API をファジー化します。</p></td>
<td align="left"><p>このテストは、その他の API をファジー テストとして同じテストを実行し、この時間、空 (長さが 0) のクエリと、無効なバッファーのアドレスをドライバー ファイルの拡張属性を取得しようとしました。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoMiscAPIWithZeroLengthTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_open_and_close_test"></span>ファジー オープンとクローズのテスト</p></td>
<td align="left"><p>このテストでは、何千もの作成-開く、閉じるシーケンスを実行します。</p>
<p>このテストの詳細については、次を参照してください。 <a href="#about-the-fuzz-open-and-close-test" data-raw-source="[About the Fuzz open and close test](#about-the-fuzz-open-and-close-test)">、ファジーについて開閉テスト</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoOpenCloseTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Query_and_Set_File_Information_test_"></span><span id="fuzz_query_and_set_file_information_test_"></span><span id="FUZZ_QUERY_AND_SET_FILE_INFORMATION_TEST_"></span>ファジー テストをクエリし、ファイル情報の設定</p></td>
<td align="left"><p>このテストでは、呼び出しを取得し、デバイスのオブジェクト、ファイル、およびボリューム情報の変更を発行します。</p>
<p>中に、<em>クエリし、ファイル情報のテストの設定</em>、によって開かれたを取得し、デバイスのオブジェクト、ファイル、およびボリュームの情報を変更するには、ファジー テスト問題呼び出し、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">を開く操作の基本的な</a>およびその他のオープンファジー サブ開きますテストで実行された操作などの操作。</p>
<p>ファジー テストの問題の各クエリまたは有効なバッファーとバッファーの長さおよびファイル情報クラスのさまざまな 1024 回以上呼び出しを設定します。 各型の 1 つの要求は、無効なバッファー ポインターと 0 個のバッファーの長さも送信されます。</p>
<p>使用する場合、 <em>ChangeBufferProtectionFlags</em>バッファー内で、保護のオプション、ファジー テストによって異なります、セキュリティ設定を設定するパラメーターは、各クエリし、呼び出しを設定します。</p>
<p>このテストでは、ファジー サブ開きますテストも実行します。</p>
<p>このテストでは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567052" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567052)"> <strong>ZwQueryInformationFile</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567096" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567096)"> <strong>ZwSetInformationFile</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567070" data-raw-source="[&lt;strong&gt;ZwQueryVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567070)"> <strong>ZwQueryVolumeInformationFile</strong></a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff567112" data-raw-source="[&lt;strong&gt;ZwSetVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567112)"> <strong>ZwSetVolumeInformationFile</strong> </a>関数。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoQueryAndSetFileInformationTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Query_and_Set_Security_test"></span><span id="fuzz_query_and_set_security_test"></span><span id="FUZZ_QUERY_AND_SET_SECURITY_TEST"></span>ファジー クエリとセキュリティの設定のテスト</p></td>
<td align="left"><p>このテストでは、セキュリティ記述子を取得し、デバイスのセキュリティ状態を変更する呼び出しを発行します。</p>
<p>中に、<em>クエリし、セキュリティのテストの設定</em>、ファジー テストは、セキュリティ記述子を取得および変更によって開かれたデバイスのセキュリティ状態への呼び出しを発行、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">を開く操作の基本的な</a>およびその他のオープンファジー サブ開きますテストで実行された操作などの操作。</p>
<p>ファジー テストの問題の各クエリまたは有効なバッファーと、さまざまなバッファーの長さとセキュリティ情報の種類 (OWNER_SECURITY_INFORMATION GROUP_SECURITY_INFORMATION、DACL_SECURITY_INFORMATION SACL_SECURITY_ 1024 回以上呼び出しを設定情報、および情報の種類がありません)。 各型の 1 つの要求は、無効なバッファー ポインターと 0 個のバッファーの長さも送信されます。</p>
<p>使用する場合、 <em>ChangeBufferProtectionFlags</em>バッファー内で、保護のオプション、ファジー テストによって異なります、セキュリティ設定を設定するパラメーターは、各クエリし、呼び出しを設定します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoQueryAndSetSecurityTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Random_FSCTL_test___Fuzz_Random_IOCTL_test_"></span><span id="fuzz_random_fsctl_test___fuzz_random_ioctl_test_"></span><span id="FUZZ_RANDOM_FSCTL_TEST___FUZZ_RANDOM_IOCTL_TEST_"></span>ファジー ランダム FSCTL テスト/ランダム IOCTL のファジー テスト</p></td>
<td align="left"><p>このテストでは、関数コード、デバイスの種類、データ転送方法、および値の指定した範囲からランダムに選択されているアクセス要件を一連の DeviceIoControl 関数の呼び出しを発行します。 呼び出しは、入力と出力バッファー有効と無効なポインターと長さをバッファリングしてからランダムに生成したコンテンツ。</p>
<p>ランダムのテスト中に、ファジー テストの問題への呼び出しの一連の<strong>DeviceIoControl</strong>関数コード、デバイスの種類、データ転送方法、および指定した範囲からランダムに選択されているアクセス要件を持つ関数値。 呼び出しは、入力と出力バッファー有効と無効なポインターと長さをバッファリングしてからランダムに生成したコンテンツ。</p>
<p>ファジー テストでは、ランダムなテストを実行中に開かれたすべてのデバイスで、<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本の開く操作</a>と追加のテストを開きます。 このテストは、次のパラメーターを使用してカスタマイズできます。</p>
<ul>
<li><p>使用<em>MinFunctionCode</em>と<em>MaxFunctionCode</em>関数の呼び出しで使用されるコードの範囲の IOCTL または FSCTL を指定するには</p></li>
<li><p>使用<em>MinDeviceType</em>と<em>MaxDeviceType</em>の呼び出しで使用されるデバイスの種類の範囲を指定するには</p></li>
<li><p>使用<em>SeedNumber</em>ルーチンを生成する乱数のシード数を指定します。</p></li>
</ul>
<p>ファジー テストを使用して、テストを使用する乱数を生成する関数を<em>シード数</em>、ランダムな番号生成アルゴリズムの数を開始します。 テスト条件を再現するを使用して、<em>シード数</em>シード数を指定するパラメーターは、元のテストの試用版で使用されました。</p>
<p>A<em>ランダムなテストを合わせた</em>はランダムなテストの一部として含まれています。 調整されたランダムなテストでは、ランダムなテストの結果を使用して、さらに詳しく IOCTL または FSCTL の要求に対するドライバーの応答を調べる。 調整されたランダムなテストでは、ランダムなテスト不足の領域とランダムなテストの呼び出しによって返される状態に基づいて予想どおり、いないにドライバーを応答でしたをプローブします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoRandomIOCTLTest, DoRandomFSCTLTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
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
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_sub-opens_test"></span>ファジー サブ開きますテスト</p></td>
<td align="left"><p>テストは、迅速な一連のデバイスの名前空間でオブジェクトを開く呼び出しを実行します。 これらの呼び出しで、デバイスで始まり、任意の名前とさまざまな長さで、コンテンツの意味がない文字列が含まれているパスを渡します。</p>
<p>中に、<em>相対開くテスト</em>、(とも呼ばれます、<em>サブ オープン テスト</em>) ファジー テストが、デバイスのオブジェクトを開こうと<a href="https://msdn.microsoft.com/library/windows/hardware/ff542068" data-raw-source="[namespace](https://msdn.microsoft.com/library/windows/hardware/ff542068)">名前空間</a>します。</p>
<p>ファジー テストをこのテストは中に、は、迅速な一連の呼び出しを使用して開かれたデバイスの名前空間でオブジェクトを開くを実行します<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">を開く操作の基本的な</a>およびその他の開く操作。 これらの呼び出しでは、ファジー テストは、デバイスで始まり、任意の名前とさまざまな長さで、コンテンツの意味がない文字列が含まれているパスを渡します。</p>
<p>このテストでは、ドライバーまたはファイル システムがその名前空間でのオープン要求を管理する方法を決定します。 具体的には、ドライバーは、名前空間でのオープン要求をサポートしていない場合、防ぐ必要があります未承認のアクセスを要求、失敗したかを使用する場合は、FILE_DEVICE_SECURE_OPEN デバイスの特性を設定して<a href="https://msdn.microsoft.com/library/windows/hardware/ff548397" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548397)"> <strong>IoCreateDevice</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff548407" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548407)"> <strong>IoCreateDeviceSecure</strong> </a>デバイス オブジェクトを作成します。</p>
<p>デバイスの名前空間の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff542068" data-raw-source="[Controlling Device Namespace Access](https://msdn.microsoft.com/library/windows/hardware/ff542068)">デバイス Namespace のアクセスを制御する</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoSubOpensTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Sub-opens_with_Streams_test"></span><span id="fuzz_sub-opens_with_streams_test"></span><span id="FUZZ_SUB-OPENS_WITH_STREAMS_TEST"></span>ストリームのテストがファジー サブ表示</p></td>
<td align="left"><p>このテストでは、さまざまなデバイス上の名前付きのデータ ストリームを開こうとします。 テストでは、一連の任意のストリーム名を使用して、コンテンツと一部のデバイスでの他の使用を有効になる可能性がある文字で。</p>
<p>中に、<em>ストリーム テスト</em>、ファジー テストは、さまざまなデバイス上の名前付きのデータ ストリームを開こうとします。 テストは、コンテンツと一部のデバイスでの他の使用を有効になる可能性がある文字で、一連の任意のストリーム名を使用します。 このテストでは、ドライバーがドライバーはサポートされておらず、データ ストリームを予測するデバイスをエクスポートする場合は特に、データ ストリームの要求を処理適切かどうかを判断します。</p>
<p>A<em>という名前のデータ ストリーム</em>ファイル オブジェクトの属性です。 場所、ファイル、コロン、およびデータ ストリーム、たとえば、"File01.txt:AccessDate"の名前の名前を記述することで、名前付きのデータ ストリームを指定する<em>AccessDate</em> 、File01.txt ファイルの属性は、名前付きのデータ ストリームです。</p>
<p>ファジー テスト レコード ストリーム名は、テストで使用します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoSubOpensWithStreamsTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Zero-Length_Buffer_FSCTL_test___Fuzz_Zero-Length_Buffer_IOCTL_test"></span><span id="fuzz_zero-length_buffer_fsctl_test___fuzz_zero-length_buffer_ioctl_test"></span><span id="FUZZ_ZERO-LENGTH_BUFFER_FSCTL_TEST___FUZZ_ZERO-LENGTH_BUFFER_IOCTL_TEST"></span>ファジー バッファー FSCTL を長さ 0 のテスト/長さ 0 のバッファー IOCTL のファジー テスト</p></td>
<td align="left"><p>このテストへの呼び出しの一連の問題、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl 関数</strong></a> 0 の入力または出力バッファー長を持つ。 テストは、別の関数コード、デバイスの種類、データ転送方法、およびアクセスの要件を使用して、さまざまなファイル システムの制御コードを生成します。</p>
<p>ファジー テストへの呼び出しの一連の問題を長さ 0 のバッファーのテスト中に、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl 関数</strong></a> 0 の入力または出力バッファー長を持つ。 テストは、別の関数コード、デバイスの種類、データ転送方法、およびアクセスの要件を使用して、さまざまな I/O 制御コードを生成します。 I/O 制御コードの内容については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543023" data-raw-source="[Defining I/O Control Codes](https://msdn.microsoft.com/library/windows/hardware/ff543023)">I/O 制御コードを定義する</a>します。</p>
<p>無効なバッファーのポインターのドライバーの処理をテストするには、これらのユーザー モードの呼び出しでバッファー ポインターのアドレスを指定高 0xFFFFFC00 などのカーネルの仮想アドレス空間)。</p>
<p>ファジー テストでは、基本および追加の開いているテスト中に開かれたすべてのデバイスでバッファーの長さ 0 のテストを実行します。 使用してこのテストをカスタマイズすることができます、 <em>MinFunctionCode</em>と<em>MaxFunctionCode</em>関数の呼び出しで使用されるコードの範囲の IOCTL または FSCTL を指定するパラメーターのコマンドと<em>MinDeviceType</em>と<em>MaxDeviceType</em>の呼び出しで使用されるデバイスの種類の範囲を指定します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>メソッドをテストします。</strong>DoZeroLengthBufferIOCTLTest、DoZeroLengthBufferFSCTLTest</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>MinDeviceType</em></p>
<p><em>MaxDeviceType</em></p>
<p><em>MinFunctionCode</em></p>
<p><em>MaxFunctionCode</em></p>
<p><em>DoPoolCheck</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>権限を借用します。</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Run_I_O_Attack"></span><span id="run_i_o_attack"></span><span id="RUN_I_O_ATTACK"></span>I/O の攻撃を実行します。</p></td>
<td align="left"><p>実行<a href="ioattack.md" data-raw-source="[I/O Attack](ioattack.md)">I/O 攻撃</a>で指定したデバイスまたはデバイス。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOAttack_DeleteDataFile.wsc</p>
<p><strong>メソッドをテストします。</strong>RunIoAttack</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-fuzz-open-and-close-test"></a>について、ファジー開閉テスト


ファジーを開くし、閉じるテストを開くと、指定したデバイスまたはデバイスのインスタンスの終了のいくつかの方法を採用しています。[オープン操作の基本的な](#basic-open-operations)、[デバイス オープン操作を直接](#direct-device-open-operations)、および[テストを開いたり閉じたり](#open-and-close-test)します。

### <a name="basic-open-operations"></a>基本のオープン操作

中に、*オープン操作の基本的な*、ファジー テストが開きますで繰り返し (作成)、指定したデバイスまたはデバイスのインスタンスは、さまざまな方法とオプションを使用して、指定されたドライバーによってエクスポートされました。

ファジー テストでは、常に、基本的なオープン操作を実行します。 それらを選択する必要はありませんし、テスト セッションから除外することはできません。

ファジー テスト システム サービスを呼び出すことによってユーザー モードで開いているすべての操作を実行します ([ZwXxx ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff567122)) デバイスに必要な。 Open の呼び出しは、デバイスへのハンドルを返します、ファジー テストはテスト セッション用に選択された他のデバイス テストを実行するのにハンドルを使用します。

基本のオープン操作の 5 つの種類があります。

-   **オープン標準です。** ファジー テストでは、デバイスを非同期的に開き、デバイスのネイティブ名のみを指定します。

-   **開くには、円記号が追加されます。** ファジー テストの問題、デバイス名の後に円記号のオープン呼び出し (\)など\\デバイス\\cdrom\\呼び出しは、デバイス内のルート ディレクトリを開くことができるようします。

    この操作は、ドライバーまたはファイル システムがその名前空間でのオープン要求を管理する方法を決定します。 具体的には、デバイスはその名前空間でのオープン要求をサポートしていない場合、ドライバー防ぐ必要があります未承認のアクセスを要求が失敗するか、ファイルを設定して\_デバイス\_SECURE\_開いているデバイス特性を呼び出すときに[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)または[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)デバイス オブジェクトを作成します。

-   **名前付きパイプとして開きます。** ファジー テストでは、デバイスを表示し、デバイスに名前付きパイプを確立します。 アクセス パラメーター (ShareAccess) は、読み取りし、書き込みに初期設定が、要求が失敗した場合に調整します。 デバイスが名前付きパイプをサポートしていない場合、要求は失敗にする必要があります。

-   **メール スロットとして開きます。** ファジー テストでは、メール スロットとして、デバイスが表示されます。 デバイスがこの種類の接続をサポートしていない場合、要求は失敗にする必要があります。

-   **接続をツリーとして開きます。** ファジー テストでは、リモート ネットワーク アクセスで使用するため、ツリーの接続とデバイスを開きます。 アクセス パラメーター (ShareAccess) は、読み取りし、書き込みに初期設定が、要求が失敗した場合に調整します。 デバイスがこの種類の接続をサポートしていない場合、要求は失敗にする必要があります。

Open の呼び出しで使用されるパラメーターによって異なります、デバイスの特性に対応し、可能性は、呼び出しが成功します。 たとえば、呼び出し、デバイスのセキュリティ要件を満たしていないため、基本的なオープン操作が失敗した場合ファジー テストによってより低いアクセスの要求でファイルを開く操作が繰り返されます。 たとえば、オープン操作が書き込みアクセス権を要求するには、セキュリティ違反のエラーが返された場合、オープンが読み取りアクセス権の要求で繰り返されます。

### <a name="direct-device-open-operations"></a>デバイスのダイレクト オープン操作

中に、*デバイス オープン操作を直接*、ファジー テスト デバイスを開きますデバイスとして、直接、ファイルとしてではなくファイル システムにします。 デバイスの直接の開く操作は、同期は常にします。 呼び出しが成功した場合、ファジー テストには、選択したその他のテストを実行する指定されたハンドルが使用されます。

### <a name="open-and-close-test"></a>オープンとクローズのテスト

中に、*オープンし、テストを閉じる*、ファジー テストが何千もの作成-開く、閉じるシーケンスを実行、複数のスレッドを作成します。 これは、それ以外の場合簡単で予想される呼び出しの特別のボリュームを処理するために、ドライバーの機能をテストします。

オープンとクローズのテストで使用される同じオプションを使用して[オープン操作の基本的な](#basic-open-operations)テストを追加の円記号で開くと、直前にこれらのテストが実行されます。

## <a name="related-topics"></a>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






