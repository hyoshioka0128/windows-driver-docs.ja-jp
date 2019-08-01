---
title: IRP ログ
description: ドライバーの検証ツールの IRP ログ機能は、ドライバーの irp の使用を監視し、IRP の使用状況を記録します。 このレコードは、WMI 情報として格納されます。
ms.assetid: 368356df-7fa7-4555-b5cf-59c26d70075e
keywords:
- IRP ログ機能 WDK ドライバー検証ツール
- DC2WMIParser ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed401d922d818de7ecb11ea630550e82a6ae1bd0
ms.sourcegitcommit: 3aee55397dda48607258697da14e11c183557603
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702168"
---
# <a name="irp-logging"></a>IRP ログ


ドライバーの検証ツールの IRP ログ機能は、ドライバーの irp の使用を監視し、IRP の使用状況を記録します。 このレコードは、WMI 情報として格納されます。

## <span id="ddk_irp_logging_tools"></span><span id="DDK_IRP_LOGGING_TOOLS"></span>


Windows Driver Kit (WDK) には、この WMI レコードをテキストファイルに変換できるツール DC2WMIParser (DC2WMIParser) が含まれています。

このドライバーの検証ツールオプションは、Windows Server 2003 以降でのみ使用できます。

### <a name="span-idthewmirecordspanspan-idthewmirecordspanthe-wmi-record"></a><span id="the_wmi_record"></span><span id="THE_WMI_RECORD"></span>WMI レコード

WMI レコードは、デバイスごとに20個を超える Irp を含みません。 20番目の IRP が記録されると、最初の IRP レコードが置き換えられます。 そのため、レコードに20個の Irp が一覧表示されている場合、これらは常に最新の20になりますが、どちらが最新であるかを知る方法はありません。

WMI レコードはメモリに格納されるため、コンピューターの再起動時に消去されます。 そのため、DC2WMIParser を使用して、この情報をファイルに保存します。

**/T**オプションを使用すると、DC2WMIParser は指定された期間、連続して実行されます。 この場合、レコードにはデバイスあたり20個を超える Irp を含めることができます (各サンプリング期間で最大20個の irp)。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーの IRP ログ機能をアクティブ化できます。

IRP ログ機能をアクティブ化するには、 [I/o 検証](i-o-verification.md)もアクティブ化する必要があります。

-   **コマンドラインで**

    コマンドラインでは、IRP ログオプションは**0x400** (ビット 10) で表されます。

    IRP ログをアクティブにするには、フラグ値0x410 を使用するか、フラグ値に0x410 を追加します。 この値は、 [i/o 検証](i-o-verification.md) (0x10) と IRP Logging (0x400) をアクティブにします。 次に、例を示します。

    ```
    verifier /flags 0x410 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動しなくても、IRP ログをアクティブ化および非アクティブ化することができます。 次に、例を示します。

    ```
    verifier /volatile /flags 0x410 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

-   **ドライバー検証マネージャーの使用**
    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  [ **IRP ログ記録**と[i/o 検証](i-o-verification.md)] を選択します。

### <a name="span-iddc2wmiparserspanspan-iddc2wmiparserspandc2wmiparser"></a><span id="dc2wmiparser"></span><span id="DC2WMIPARSER"></span>DC2WMIParser

DC2WMIParser は、ドライバーの検証ツールによって作成された WMI IRP レコードを収集し、このログをテキストファイルに変換するツールです。

DC2WMIParser 構文は次のとおりです。

```
dc2wmiparser [/f File] [/t Time]
```

パラメーターの意味は次のとおりです。

<span id="_________fFile"></span><span id="_________ffile"></span><span id="_________FFILE"></span> **/f**_ファイル_  
書き込むログファイルの完全なパスとファイル名を指定します。 相対パスは、現在のディレクトリに対して相対的に取得されます。 これを省略すると、現在のディレクトリのファイル名 dc2verifier が使用されます。

<span id="_tTime"></span><span id="_ttime"></span><span id="_TTIME"></span> **/t**_時刻_  
DC2WMIParser が継続して実行される時間の長さを分単位で指定します。 *時刻*が0の場合、DC2WMIParser は、ドライバー検証ツールによって既に格納されているすべての WMI IRP 情報を記録してから、を終了します。 *Time*が正の値に設定されている場合、DC2WMIParser は指定された時間だけ実行を続け、新しい情報を格納します。 既定値は 0 です。

### <a name="span-idformatofdc2wmiparserlogfilesspanspan-idformatofdc2wmiparserlogfilesspanformat-of-dc2wmiparser-log-files"></a><span id="format_of_dc2wmiparser_log_files"></span><span id="FORMAT_OF_DC2WMIPARSER_LOG_FILES"></span>DC2WMIParser ログファイルの形式

DC2WMIParser によって生成されるファイルは、ASCII テキストファイルです。

このファイルの最初の行には、ファイルに記録されたデバイスの数を表す10進数が含まれています。

最初の行の後に、ファイルはセクションに分割されます。各セクションでは、1つのデバイスについて説明します。

デバイスごとに、形式は次のとおりです。

-   **1行:** デバイス名。

-   **1行:** このデバイスを対象とするデバイスの種類と機能の数を指定する10進数。

-   **デバイスの種類と機能ごとに1行。** コンマで区切られた3つの16進数。 これらは、デバイスの種類と、このレコードに記録された最下位および最高の関数を表します。

-   **デバイスの種類と機能ごとに、1つの行グループに含まれます。**
    -   現在のデバイスの種類の Ioctl の数を指定する10進数の単一行。
    -   各 IOCTL の1行。 これらの各行には、コンマで区切られた6つの16進数が含まれています。 デバイスの種類、関数、メソッド、アクセス、入力バッファーの長さ、および出力バッファーの長さを指定します。

DC2WMIParser ログファイルのサンプルを次に示します。 実際のファイルには、スペース、コメント、または空白行は含まれませんが、この例ではより明確になるように追加されています。

```
2           There are two devices described by this log file.

The first device begins here:

  DP(1)0x7e00-0x21dbda400+3   Device name of the first device
  2                           Number of device type IOCTLs targeted at this device

    7,12,12                     First targeted device: device type 7, low function 12, high function 12
    2d,420,420                  Second targeted device: device type 2d, low function 420, high function 420

    1                           Number of IOCTLs for first targeted  device (type 7)
      7,12,0,0,90,0               Device type 7, function 12, method 0, access 0, inbuflen 90, outbuflen 0
    1                           Number of IOCTLs for second targeted device (type 2d)
      2d,420,0,0,c,0              Device type 2d, function 420, method 0, access 0, inbuflen c, outbuflen 0

The second device begins here:

  DP(1)0x7e00-0x21dbda400+2   Device name of the second device
  2                           Number of device type IOCTLs targeted at this device

    7,12,12                     First targeted device: device type 7, low function 12, high function 12
    2d,420,420                  Second targeted device: device type 2d, low function 420, high function 420


    1                           Number of IOCTLs for first targeted  device (type 7)
      7,12,0,0,90,0               Device type 7, function 12, method 0, access 0, inbuflen 90, outbuflen 0
    1                           Number of IOCTLs for second targeted device (type 2d)
      2d,420,0,0,c,0              Device type 2d, function 420, method 0, access 0, inbuflen c, outbuflen 0
```

 

 





