---
title: IRP ログ
description: Driver Verifier の IRP のログ記録機能は Irp のドライバーの使用を監視し、IRP の使用状況の記録します。 このレコードは、WMI 情報として格納されます。
ms.assetid: 368356df-7fa7-4555-b5cf-59c26d70075e
keywords:
- WDK の Driver Verifier IRP のログ記録機能
- DC2WMIParser ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e3cdc8267cf6727e58c6891ecdbe30f2b52114
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350517"
---
# <a name="irp-logging"></a>IRP ログ


Driver Verifier の IRP のログ記録機能は Irp のドライバーの使用を監視し、IRP の使用状況の記録します。 このレコードは、WMI 情報として格納されます。

## <span id="ddk_irp_logging_tools"></span><span id="DDK_IRP_LOGGING_TOOLS"></span>


Windows Driver Kit (WDK) DC2WMIParser ツールが含まれています (dc2wmiparser.exe) この WMI レコードをテキスト ファイルに変換することができます。

このドライバーの検証ツールのオプションは、Windows Server 2003 で使用可能な以降のみです。

### <a name="span-idthewmirecordspanspan-idthewmirecordspanthe-wmi-record"></a><span id="the_wmi_record"></span><span id="THE_WMI_RECORD"></span>WMI レコード

WMI のレコードでは、デバイスごとに 20 を超える Irp は含まれません。 21 番目 IRP が記録されると、最初の IRP レコードが置き換えられます。 レコードには、20 の Irp が一覧表示する場合、は、これらは、常に最新の 20 が次のうち最新のものを把握する方法はありません。

WMI のレコードは、メモリに保存される、ために、コンピューターが再起動されると消去されます。 そのため、DC2WMIParser を使用して、この情報をファイルに保存します。

使用する場合、 **/t**オプション、DC2WMIParser が実行する継続的に、指定された期間。 このような状況でレコードがデバイス (サンプリング期間ごとに最大 20 の Irp) あたり 20 を超える Irp を含めることができます。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの IRP のログ記録機能をアクティブにできます。

IRP のログ記録機能をアクティブ化する必要がありますもアクティブ化する[I/O の検証](i-o-verification.md)です。

-   **コマンドラインで**

    によって表される IRP のログ記録オプションをコマンドラインで**0x400** (ビット 10)。

    IRP のログ記録を有効にするには、0x410 のフラグの値を使用して、または 0x410 をフラグ値に追加します。 この値をアクティブに[I/O の検証](i-o-verification.md) (0x10) IRP のログ記録 (0x400) とします。 次に、例を示します。

    ```
    verifier /flags 0x410 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows Vista と Windows の以降のバージョンでもアクティブ化し、追加することで、コンピューターを再起動しなくても IRP のログ記録を非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x410 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

-   **ドライバー検証マネージャーを使用します。**
    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) **IRP のログ記録**と[I/O の検証](i-o-verification.md)です。

### <a name="span-iddc2wmiparserspanspan-iddc2wmiparserspandc2wmiparser"></a><span id="dc2wmiparser"></span><span id="DC2WMIPARSER"></span>DC2WMIParser

DC2WMIParser は、Driver Verifier で作成される WMI IRP のレコードを収集するツールは、このログをテキスト ファイルに変換します。

DC2WMIParser 構文は次のとおりです。

```
dc2wmiparser [/f File] [/t Time]
```

パラメーターには、次の意味があります。

<span id="_________fFile"></span><span id="_________ffile"></span><span id="_________FFILE"></span> **/f * * * ファイル*  
書き込まれるログ ファイルのファイル名と完全なパスを指定します。 現在のディレクトリを基準とした相対パスが表示されます。 これを省略した場合は、現在のディレクトリにファイル名 dc2verifier.act が使用されます。

<span id="_tTime"></span><span id="_ttime"></span><span id="_TTIME"></span>**/t * * * 時間*  
DC2WMIParser は引き続き実行を分単位で時間の長さを指定します。 場合*時間*が 0 に等しい、DC2WMIParser はドライバーの検証ツールによって既に格納されているすべての WMI IRP 情報を記録し、終了します。 場合*時間*設定は正の値に DC2WMIParser は引き続き実行時間を指定された長さに対してが到着すると、新しい情報を格納します。 既定値は 0 です。

### <a name="span-idformatofdc2wmiparserlogfilesspanspan-idformatofdc2wmiparserlogfilesspanformat-of-dc2wmiparser-log-files"></a><span id="format_of_dc2wmiparser_log_files"></span><span id="FORMAT_OF_DC2WMIPARSER_LOG_FILES"></span>DC2WMIParser ログ ファイルの形式

DC2WMIParser によって生成されたファイルは、ASCII テキスト ファイルです。

このファイルの最初の行には、ファイルに記録するデバイスの数を表す 10 進数が含まれています。

最初の行には、ファイルはセクションに分かれています各セクションでは、1 つのデバイスについて説明します。

各デバイス形式は次のとおりです。

-   **1 行の場合。** デバイスの名前。

-   **1 行の場合。** 指定数のデバイスの種類で関数がこのデバイスを対象となる 10 進数。

-   **各デバイスの種類と関数の 1 つの行。** コンマで区切られた、3 つ 16 進数の数値。 これらは、デバイスの種類とこのレコードに記録された最低と最高の関数を表します。

-   **各デバイスの種類と関数の線の 1 つのグループ。**
    -   現在のデバイスの種類の Ioctl の数を指定する 10 進数で、1 行。
    -   各 IOCTL の 1 つの行。 これらの行には、コンマで区切られた 6 桁の 16 進数字が含まれています。 これらのデバイスの種類、関数、メソッド、アクセス、入力のバッファーの長さおよび出力バッファーの長さを指定します。

サンプル DC2WMIParser ログ ファイルを次に示します。 実際のファイルではありません、空白、コメント、または空白の行が、これらがより明確にするには、この例に追加されました。

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

 

 





