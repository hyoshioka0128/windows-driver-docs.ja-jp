---
title: 15 の例を使用してオブジェクト参照のトレース
description: 15 の例を使用してオブジェクト参照のトレース
ms.assetid: 3c6102e6-4dac-4d90-ab8f-162dd6d8adf9
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0730f0242c1011826bfbf037f1879b81a8db2823
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347758"
---
# <a name="example-15-using-object-reference-tracing"></a>例 15:オブジェクト参照トレースを使用する


オブジェクト参照のトレースは、オブジェクトが参照されているか、逆参照するときに、シーケンシャルなスタック トレースを記録する Windows 機能です。 クラッシュまたはメモリ リークにつながる可能性があるオブジェクトの処理でエラーを検出するために設計されています。 これらのエラーの一部が一貫して表示されないため、検出を困難にします。 詳細については、次を参照してください。[オブジェクト参照トレース](object-reference-tracing.md)します。

オブジェクト参照のトレースを構成を使用して、**グローバル フラグ** ダイアログ ボックスまたはコマンド プロンプトでします。 次の例では、コマンド プロンプトを使用します。 使用方法について、**グローバル フラグ**オブジェクト参照のトレースを構成するを参照してください ダイアログ ボックス[オブジェクト参照トレースの構成](configuring-object-reference-tracing.md)します。

Gflags を使用して、有効化、無効にするには、オブジェクト参照のトレースを構成することができます。 プロセスは次のとおりです。

-   **Gflags を使用して、オブジェクト参照のトレースを有効に**レジストリまたはカーネル (実行時) フラグの設定として。 設定をレジストリに追加する場合は、トレースを開始するコンピューターを再起動する必要があります。 設定の実行時バージョンを有効にした場合は、トレースは、すぐに開始がシャット ダウンまたは再起動するときに、レジストリ キーのトレースの設定元に戻します。

-   **問題のあるオブジェクトを作成するプロセスを開始**します。 トレースには、トレースが開始後に開始されたプロセスによって作成されたオブジェクトのみが含まれます。 場合は、プロセスの開始時に、または再起動した後すぐをレジストリにトレースの設定を追加し、システムを再起動します。

-   **使用して、** [ **! obtrace** ](-obtrace.md) **デバッガー拡張機能**トレースを表示します。 使用することが、オブジェクトが破棄されるまで既定では、トレースが保持される、 **/p**トレースが無効になるまで、トレースを維持するためにパラメーター。

-   **Gflags を使用して、オブジェクト参照のトレースを無効に**.in、レジストリまたはカーネル フラグ (実行時) に設定します。 レジストリから設定を削除する場合は、トレースを終了するコンピューターを再起動する必要があります。 設定の実行時バージョンを無効にした場合、すぐにトレースの終了がシャット ダウンまたは再起動するときに、レジストリのトレースの設定元に戻します。

これらの例では、Gflags を使用して有効にして、オブジェクト参照のトレースを無効にする方法を示します。 \\

### <a name="span-idenableruntimetracingspanspan-idenableruntimetracingspanenable-run-time-tracing"></a><span id="enable_run_time_tracing"></span><span id="ENABLE_RUN_TIME_TRACING"></span>実行時のトレースを有効にします。

次のコマンドは、オブジェクト参照のトレースを有効、コマンド プロンプトでします。 コマンドを使用して、 **/ko**パラメーターをカーネル (実行時) フラグの設定とオブジェクト参照の追跡を有効にします。 コマンドを使用して、 **/t**プール タグを指定するパラメーター **Tag1**と**Fred**します。 その結果、すべてのオブジェクトを作成した**Tag1**または**Fred**がトレースされます。

```console
gflags /ko /t Tag1;Fred
```

コマンドは、カーネル フラグ (実行時) の設定を変更、ため、オブジェクト参照のトレースが直ちに開始します。 トレースは、プール タグのすべてのオブジェクトが含まれます**Tag1**または**Fred**コマンドが送信された後に起動するプロセスによって作成されました。

Gflags は、次のメッセージを出力することによって応答します。

```console
Running Kernel Settings :
Object Ref Tracing Enabled
        Temporary Traces
        Pool Tags: Tag1;Fred
        Process Name: All Processes
```

このメッセージは、オブジェクト参照のトレースが有効になっていることを示します。 "一時 Traces"では、オブジェクトが破棄されるときに、トレースのすべてのレコードが削除されたことを示します。 トレースを「永続的な」するためには、使用、 **/p**パラメーターで、オブジェクト参照のトレースが無効になっているか、コンピューターをシャット ダウンまたは再起動するまで、トレース データを保持する Windows に指示します。

### <a name="span-idenabletracingintheregistryspanspan-idenabletracingintheregistryspanenable-tracing-in-the-registry"></a><span id="enable_tracing_in_the_registry"></span><span id="ENABLE_TRACING_IN_THE_REGISTRY"></span>レジストリでのトレースを有効にします。

次のコマンドは、オブジェクト参照のトレースの構成をレジストリに追加します。 コンピューターを再起動するときに構成されたトレースを開始します。

コマンドを使用して、 **/ro**パラメーターはレジストリ設定としてオブジェクト参照のトレースを有効にします。 コマンドを使用して、 **/i** notepad.exe のプロセスを指定して、 **/t**プール タグを指定するパラメーター **Tag1**と**Fred**します。 メモ帳で作成されるすべてのオブジェクトの処理結果として、 **Tag1**または**Fred**プール タグがトレースされます。 コマンドを使用しても、 **/p**パラメーターで、トレースが無効になるまで、トレース データを保持します。

```console
gflags /ro /t Tag1;Fred /i Notepad.exe /p
```

コマンドを送信するときに、Gflags はレジストリに情報を格納します。 ただし、コンピューターを再起動するまで、レジストリ設定は有効ではない、ためこのオブジェクトの参照をトレースが構成されているがまだ開始されていません。

Gflags は、次のメッセージを出力することによって応答します。

```console
Boot Registry Settings :
Object Ref Tracing Enabled
        Permanent Traces
        Pool Tags: Tag1;Fred
        Process Name: Notepad.exe
```

メッセージは、レジストリにオブジェクト参照のトレースが有効になっていることを示します。 「永続的なトレース」では、シャット ダウンするか、コンピューターを再起動するまでに、トレース データを保持することを示します。 メッセージには、プール タグとトレースはイメージ ファイルの名前も一覧表示されます。

### <a name="span-iddisplaytheobjectreferencetracingconfigurationspanspan-iddisplaytheobjectreferencetracingconfigurationspandisplay-the-object-reference-tracing-configuration"></a><span id="display_the_object_reference_tracing_configuration"></span><span id="DISPLAY_THE_OBJECT_REFERENCE_TRACING_CONFIGURATION"></span>トレースの構成のオブジェクト参照を表示します。

現在有効なまたはコンピューターを再起動したときに使用するレジストリに格納されて、オブジェクト参照のトレース構成を表示できます。

この例では、レジストリに格納されている 1 つのオブジェクト参照のトレースの構成と実行時用に構成された別の 1 つ。 実行時のトレースはすぐに開始されます (および、任意のレジストリ設定が上書きされます)。 ただし、システムを再起動する場合、実行時の設定は失われ、オブジェクト参照のトレース セッションのレジストリ設定が有効になります。

次のコマンドは、実行時のオブジェクト参照のトレースの構成を表示します。 使用して、 **/ko**他のパラメーターのないパラメーター。

```console
gflags /ko
```

```console
Running Kernel Settings :
Object Ref Tracing Enabled
        Temporary Traces
        Pool Tags: Tag1;Fred
        Process Name: All Processes
```

オブジェクト参照のトレースが有効な場合、この例では、表示される設定には進行中のトレースについて説明します。

次のコマンドは、レジストリに格納されているオブジェクトの参照のトレースの構成データを表示します。 使用して、 **/ro**他のパラメーターのないパラメーター。

```console
gflags /ro
```

応答、Gflags はレジストリに格納されたデータを表示します。

```console
Boot Registry Settings :
Object Ref Tracing Enabled
        Permanent Traces
        Pool Tags: Tag1;Fred
        Process Name: Notepad.exe
```

オブジェクト参照のトレースの構成をレジストリに追加するため、コンピューターを再起動した場合、gflags/ro コマンドへの応答に表示される設定には、進行中のトレースがについて説明します。 ただし、まだ再起動していない、または、再起動しますが、実行時のオブジェクト参照のトレースを開始し (**/ko**)、レジストリに格納されている設定が現在有効なが、もう一度で有効にするはシステムを再起動する場合。

### <a name="span-iddisableobjectreferencetracingspanspan-iddisableobjectreferencetracingspandisable-object-reference-tracing"></a><span id="disable_object_reference_tracing"></span><span id="DISABLE_OBJECT_REFERENCE_TRACING"></span>オブジェクト参照のトレースを無効にします。

実行時 (カーネル フラグ) を無効にするとすぐにオブジェクト参照のトレース設定、トレースを停止します。 レジストリ内のオブジェクト参照のトレース設定を無効にすると、コンピューターを再起動すると、トレースを停止します。

次のコマンドは、実行時のオブジェクト参照のトレースを無効にします。 使用して、 **/d**パラメーターをすべての設定を無効にします。 設定を無効にすることはできません選択的にします。

```console
gflags /ko -d
```

コマンドが成功した場合、Gflags は、次のメッセージを返します。

```console
Running Kernel Settings :
Object Ref Tracing Disabled
```

次のコマンドは、実行時のオブジェクト参照のトレースを無効にします。

次のコマンドは、レジストリ内のオブジェクト参照のトレース設定を無効にします。 使用して、 **/d**パラメーターをすべての設定を無効にします。 設定を無効にすることはできません選択的にします。 このコマンドは、コンピューターを再起動すると効果的です。

```console
gflags /ro -d
```

コマンドが成功した場合、Gflags は、次のメッセージを返します。

```console
Boot Registry Settings :
Object Ref Tracing Disabled
```

 

 





