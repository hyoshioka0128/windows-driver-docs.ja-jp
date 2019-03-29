---
title: XPS ドライバー ドキュメント イベント
description: XPS ドライバー ドキュメント イベント
ms.assetid: 240e14d1-d8ee-403c-b728-b14941775634
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、イベント
- WDK XPSDrv イベント
- WDK XPSDrv 通知
- DrvDocumentEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8d1d67663b6d33f8d8d144636ac3b7531a47399
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574236"
---
# <a name="xps-driver-document-events"></a>XPS ドライバー ドキュメント イベント


Microsoft Windows Presentation Foundation (WPF) の印刷のサポートは、GDI 印刷のサポートが GDI 印刷ドライバーに通知を送信する方法と同様に、ドキュメント スプール中の通知イベントを XPSDrv プリンター ドライバーに送信します。 WPF の印刷のサポートも使用して同じ**DrvDocumentEvent** GDI 印刷のサポートを使用して、DDI 関数が新しいイベントがイベントの XPS ドキュメントの処理をサポートするために定義されています。 GDI 印刷のサポートは引き続き発行**DrvDocumentEvent** GDI ベースの印刷ドライバーを XPSDrv イベント ハンドラーは、Microsoft Win32 アプリケーションの印刷用のドライバーを印刷します。

### <a name="drvdocumentevent-event-handler-overview"></a>DrvDocumentEvent イベント ハンドラーの概要

かどうか、必要に応じて XPSDrv プリンター ドライバーをエクスポートできます、 **DrvDocumentEvent**切片ドキュメントの関数を処理するには構成モジュールからイベント ハンドラー。 新しい XPS ドキュメントに関連するイベントが始まるシンボリック名によって識別されます"DOCUMENTEVENT\_XPS\_"。

WPF の印刷の呼び出しをサポートする、 **DrvDocumentEvent** XPSDrv プリンター ドライバー印刷ドキュメントをスプール中の関数。 各呼び出しは、プロセスのさまざまなステップで発生します。 各呼び出しの処理手順がの値によって識別される、 *iEsc*引数。 によって参照されているバッファーの内容、 *pvIn*と*pvOut*処理手順によって、引数が異なります。

このトピックでは、次のサブセクションでは、WPF の印刷のサポートを生成する XPS ドキュメントの処理イベントのみを説明します。

### <a name="drvdocumentevent-event-handler-description"></a>DrvDocumentEvent イベント ハンドラーの説明

**DrvDocumentEvent**イベント ハンドラーに次の呼び出し元の形式。 このセクションでは、コードとパラメーターの定義では、参照専用です。

```cpp
INT
  DrvDocumentEvent(
    HANDLE  hPrinter,
    HDC  hdc,
    int  iEsc,
    ULONG  cbIn,
    PVOID  pvIn,
    ULONG  cbOut,
    PVOID  pvOut
    );
```

### <a name="parameters"></a>パラメーター

<a href="" id="hprinter"></a>*hPrinter*  
プリンター ハンドルが WPF の印刷のサポートを提供します。

<a href="" id="hdc"></a>*hdc*  
呼び出し元が指定したデバイス コンテキストを処理する、**フォーマット**呼び出しが生成されます。 (**フォーマット**については、Microsoft Windows SDK ドキュメントで説明します)。このパラメーターがの場合は 0 *iEsc* DOCUMENTEVENT に設定されている\_CREATEDCPRE します。

ドキュメントを印刷する場合、システムは XPS と GDI の両方のドキュメントのイベントと同じ値を使用します。 ドライバーのこの類似性に注意してくださいし、に基づいて、ジョブの種類を決定する必要があります、 *hdc*します。 *hdc*は無効と等しく\_処理\_すべて DOCUMENTEVENT 値\_XPS\_*Xxx*イベント。 このチェックを適切に解釈が決定されます、 **DrvDocumentEvent**イベント値は、呼び出し元アプリケーションに基づいています。 このチェックは、XPSDrv プリンター ドライバーだけに適用されます。

<a href="" id="iesc"></a>*iEsc*  
処理するイベントを識別する呼び出し元が指定のエスケープ コードです。 このパラメーターは、次の整数定数のいずれかを指定できます。

<a href="" id="documentevent-queryfilter-"></a>DOCUMENTEVENT\_クエリ フィルター   
WPF の印刷サポートは、ドライバーが応答するイベントを処理して XPS ドキュメントの一覧については、印刷ドライバーを照会するには、このイベントを送信します。 このイベントは、XPS ドキュメントに関連するその他のイベントの前に発行されます。

<a href="" id="documentevent-xps-addfixeddocumentsequencepre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRE  
WPF の印刷サポートは、FixedDocumentSequence XPS のスプール ファイルに追加する前に、このイベントを送信します。

<a href="" id="documentevent-xps-addfixeddocumentsequencepost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPOST  
WPF の印刷サポートは、FixedDocumentSequence XPS のスプール ファイルに追加した後にこのイベントを送信します。

<a href="" id="documentevent-xps-addfixeddocumentpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRE  
WPF の印刷サポートは、FixedDocument XPS のスプール ファイルに追加する前に、このイベントを送信します。

<a href="" id="documentevent-xps-addfixeddocumentpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPOST  
WPF の印刷サポートは、FixedDocument XPS のスプール ファイルに追加した後にこのイベントを送信します。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE  
WPF では、PrintTicket を FixedDocumentSequence (ジョブ レベル) に追加しようとしています。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST  
WPF は、ドライバーは、対応する返しますテストケースを解放する必要があります**DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE**イベント。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE  
WPF では、PrintTicket を FixedDocument (ドキュメント レベル) に追加しようとしています。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOST  
WPF は、ドライバーで対応する DOCUMENTEVENT で返されるデータを解放する必要があります\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE イベント。

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE  
WPF では、PrintTicket を FixedPage (ページ レベル) に追加しようとしています。

<a href="" id="documentevent-xps-addfixedpageprintticketpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOST  
WPF は、ドライバーで対応する DOCUMENTEVENT で返されるデータを無料\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE イベント。

<a href="" id="documentevent-xps-canceljob"></a>DOCUMENTEVENT\_XPS\_CANCELJOB  
WPF の印刷サポートは、[キャンセル] ジョブの操作を呼び出す前に、このイベントを送信します。

<a href="" id="documentevent-xps-commitjob"></a>DOCUMENTEVENT\_XPS\_COMMITJOB  
WPF では、日付を現在のファイルに書き込みが完了しました。

<a href="" id="cbin"></a>*cbIn*  
バッファーのバイト単位のサイズを*pvln*パラメーターの参照。 この値は WPF の印刷のサポートによって提供され、イベント ハンドラーによって読み取られました。

<a href="" id="pvin"></a>*pvIn*  
呼び出し元が指定のポインター。 このパラメーターの使用に依存、 *iEsc*値を次に示します。 (、DOCUMENTEVENT の\_XPS\_*Xxx* 、この一覧に表示されていないイベント*pvIn*は使用されません)。

<a href="" id="documentevent-queryfilter"></a>DOCUMENTEVENT\_クエリ フィルター  
*pvIn* PDOCEVENT を指す\_フィルター構造 (同じ DOCUMENTEVENT です\_QUERYFILTER)。

<a href="" id="documentevent-xps-addfixeddocumentsequencepre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRE  
*pvIn*ポイント PrintPropertiesCollection 構造体 (Winspool.h を参照してください) を格納している 3 つのプロパティ。

-   EscapeCode EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。 EscapeCode は、イベント値です。

-   JobIdentifier EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。 JobIdentifier は GetJob() を呼び出すために必要な ID および**SetJob**()。

-   JobName は、これは、EPrintPropertyType:: kPropertyTypeString (UNICODE) 値。

<a href="" id="documentevent-xps-addfixeddocumentsequencepost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPOST  
同じ DOCUMENTEVENT です\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRE します。

<a href="" id="documentevent-xps-addfixeddocumentpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRE  
*pvIn*ポイント PrintPropertiesCollection 構造体 (Winspool.h を参照してください) を格納している 2 つのプロパティ。

-   EscapeCode EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。 EscapeCode は、イベント値です。

-   DocumentNumber EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。

<a href="" id="documentevent-xps-addfixeddocumentpost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPOST  
同じ DOCUMENTEVENT です\_XPS\_ADDFIXEDDOCUMENTPRE します。

<a href="" id="documentevent-xps-addfixedpagepre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRE  
*pvIn*ポイント PrintPropertiesCollection 構造体 (Winspool.h を参照してください) を格納している 2 つのプロパティ。

-   EscapeCode EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。

-   PageNumber EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。

<a href="" id="documentevent-xps-addfixedpagepost"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPOST  
同じ DOCUMENTEVENT です\_XPS\_ADDFIXEDPAGEPRE します。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE  
*pvIn*ポイント PrintPropertiesCollection 構造体 (Winspool.h を参照してください) を格納している 4 つのプロパティ。

-   EscapeCode EPrintPropertyType::kPropertyTypeInt32 (ULONG) です。 EscapeCode は、イベント値です。

-   JobIdentifier EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。

-   JobName は、これは、EPrintPropertyType:: kPropertyTypeString (UNICODE) 値。

-   これは、EPrintPropertyType PrintTicket、:: kPropertyTypeByte 値。

PrintPropertiesCollection 構造と、"PRE"イベントには、そのプロパティを割り当てるし、対応する"POST"イベントを解放する必要があります。 設定することができます*pvOut*に**NULL**をイベントをサポートするが、特定のドキュメントまたはページの PrintTicket を変更する必要がないことを示します。 プラグインは「プレ」と"POST"イベントの間をアンロードことはありません。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOS  
*pvIn* DOCUMENTEVENT から pvOut として同じポインター\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE

ドライバーを解放する必要があります*pvIn*します。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE  
*pvIn*ポイント PrintPropertiesCollection 構造体 (Winspool.h を参照してください) を格納している 3 つのプロパティ。

-   EscapeCode EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。 EscapeCode は、イベント値です。

-   DocumentNumber EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。

-   これは、EPrintPropertyType PrintTicket、:: kPropertyTypeByte 値。

PrintPropertiesCollection 構造と、"PRE"イベントには、そのプロパティを割り当てるし、対応する"POST"イベントを解放する必要があります。 設定することができます*pvOut*に**NULL**をイベントをサポートするが、特定のドキュメントまたはページの PrintTicket を変更する必要がないことを示します。 プラグインは「プレ」と"POST"イベントの間をアンロードことはありません。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOS  
*pvIn*として同じポインター *pvOut* DOCUMENTEVENT から\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE します。

ドライバーを解放する必要があります*pvIn*します。

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE  
*pvIn*ポイント PrintPropertiesCollection 構造体 (Winspool.h を参照してください) を格納している 3 つのプロパティ。

-   EscapeCode EPrintPropertyType::kPropertyTypeInt32 (ULONG) 値です。 EscapeCode は、イベント値です。

-   PageNumber は EPrintPropertyType::kPropertyTypeInt32 (ULONG)。

-   これは、EPrintPropertyType PrintTicket、:: kPropertyTypeByte します。

PrintPropertiesCollection 構造と、"PRE"イベントには、そのプロパティを割り当てるし、対応する"POST"イベントを解放する必要があります。 設定することができます*pvOut*に**NULL**をイベントをサポートするが、特定のドキュメントまたはページの PrintTicket を変更する必要がないことを示します。 プラグインは「プレ」と"POST"イベントの間をアンロードことはありません。

<a href="" id="documentevent-xps-addfixedpageprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOS  
*pvIn*として同じポインター *pvOut* DOCUMENTEVENT から\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE します。

ドライバーを解放する必要があります*pvIn*します。

<a href="" id="documentevent-xps-canceljob"></a>DOCUMENTEVENT\_XPS\_CANCELJOB  
*pvIn*は**NULL**します。

<a href="" id="cbout"></a>*cbOut*  
場合、 *iEsc*パラメーターが含まれる**DOCUMENTEVENT\_おいた QUERYFILTER**、WPF の印刷サポートの提供、バッファーのサイズ、 *pvOut*パラメーター内の参照、 *cbOut*パラメーター。 その他のすべての値の*iEsc*、 *cbOut*は使用されません。

<a href="" id="--------pvout"></a> pvOut  
WPF の印刷をサポートするバッファーへのポインターを提供します。 バッファーのサイズと内容は、の値によって異なります、 *iEsc*パラメーター。 次の一覧の内容を記述する、 *pvOut*各バッファー *iEsc*値。

<a href="" id="documentevent-queryfilter-"></a>DOCUMENTEVENT\_クエリ フィルター   
DOCEVENT を格納しているバッファーへの呼び出し元が指定したポインター\_フィルター構造体。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpre-"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE   
ポインターを PrintPropertiesCollection (Winspool.h を参照してください) を含む構造型 EPrintPropertyType::kPropertyTypeBuffer の"PrintTicket"プロパティです。 このプロパティが存在するでは常にします。 PrintTicket が利用できない場合 PrintPropertyValue.propertyBlob.pBuf の値は**NULL**します。

プロパティには、Microsoft Windows Presentation Foundation (WPF) は、1 つの代わりに、PrintTicket を使用する、XML PrintTicket が含まれていますが、 **XPSDocumentWriter**呼び出し元の提供が終了します。 (場合*pvOut*は**NULL** 、プロパティが存在しないまたはプロパティのデータが**NULL**WPF は、呼び出し元が指定 PrintTicket を使用します)。

このイベントが処理されると、WPF が呼び出す**DocumentEvent** DOCUMENTEVENT で\_XPS\_を解放するドライバーの ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST *pvOut*します。

<a href="" id="documentevent-xps-addfixeddocumentsequenceprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOS  
**NULL**

<a href="" id="documentevent-xps-addfixeddocumentprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPRE  
ポインターを PrintPropertiesCollection (Winspool.h を参照してください) を含む構造型 EPrintPropertyType::PropertyTypeBuffer の"PrintTicket"プロパティです。 このプロパティは、常に存在します。 PrintTicket が使用できない場合の値**PrintPropertyValue**. propertyBlob.pBuf は**NULL**します。

プロパティには、WPF は、1 つの代わりに、PrintTicket を使用する、XML PrintTicket が含まれていますが、 **XPSDocumentWriter**呼び出し元の提供が終了します。 (場合*pvOut*は**NULL** 、プロパティが存在しないまたはプロパティのデータが**NULL**WPF は、呼び出し元が指定 PrintTicket を使用します)。

このイベントが処理されると、WPF が呼び出す**DocumentEvent** DOCUMENTEVENT で\_XPS\_を解放するドライバーの ADDFIXEDDOCUMENTPRINTTICKETPOST *pvOut*します。

<a href="" id="documentevent-xps-addfixeddocumentprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDDOCUMENTPRINTTICKETPOS  
**NULL**

<a href="" id="documentevent-xps-addfixedpageprintticketpre"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPRE  
ポインターを PrintPropertiesCollection (Winspool.h を参照してください) を含む構造型 EPrintPropertyType の"PrintTicket"プロパティ。PropertyTypeBuffer します。 このプロパティが存在するでは常にします。 PrintTicket が使用できない場合の値**PrintPropertyValue**. propertyBlob.pBuf は**NULL**します。

プロパティには、WPF は、1 つの代わりに、PrintTicket を使用する、XML PrintTicket が含まれていますが、 **XPSDocumentWriter**呼び出し元の提供が終了します。 (場合*pvOut*は**NULL** 、プロパティが存在しないまたはプロパティのデータが**NULL**WPF は、呼び出し元が指定 PrintTicket を使用します)。

このイベントが処理されると、WPF が呼び出す**DocumentEvent** DOCUMENTEVENT で\_XPS\_を解放するドライバーの ADDFIXEDPAGEPRINTTICKETPOST *pvOut*します。

<a href="" id="documentevent-xps-addfixedpageprintticketpos"></a>DOCUMENTEVENT\_XPS\_ADDFIXEDPAGEPRINTTICKETPOS  
**NULL**

### <a name="return-value"></a>戻り値

**DrvDocumentEvent**値は次のいずれかを返します。

<a href="" id="documentevent-success"></a>DOCUMENTEVENT\_成功  
ドライバーは、エスケープを正常に処理するコード*iEsc*識別します。

<a href="" id="documentevent-failure"></a>DOCUMENTEVENT\_エラー  
ドライバーは、エスケープをサポートしているコードを*iEsc*識別しますが、障害が発生しました。

<a href="" id="documentevent-unsupported"></a>DOCUMENTEVENT\_サポートされていません  
ドライバーは、エスケープをサポートしていないコードを*iEsc*識別します。

### <a name="xps-document-event-structures-and-event-code-values"></a>XPS ドキュメントのイベントの構造とイベント コード値

次のコード例では、構造と新しい XPS ドキュメントのイベントを使用する定数を示します。

```cpp
//
// structures used in XPS Document events
//
 
typedef enum
    {
        kPropertyTypeString = 1,
        kPropertyTypeInt32,
        kPropertyTypeInt64,
        kPropertyTypeByte,
        kPropertyTypeTime,
        kPropertyTypeDevMode,
        kPropertyTypeSD,
        kPropertyTypeNotificationReply,
        kPropertyTypeNotificationOptions,

    } EPrintPropertyType;

    typedef struct
    {
        EPrintPropertyType       ePropertyType;
        union
        {
            BYTE                 propertyByte;
            PWSTR                propertyString;
            LONG                 propertyInt32;
            LONGLONG             propertyInt64;
            struct {
                DWORD  cbBuf;
                LPVOID pBuf;
            }                    propertyBlob;
        } value;

    }PrintPropertyValue;

    typedef struct
    {
        WCHAR*                  propertyName;
        PrintPropertyValue      propertyValue;

    }PrintNamedProperty;

    typedef struct
    {
        ULONG                   numberOfProperties;
        PrintNamedProperty*     propertiesCollection;

    }PrintPropertiesCollection;
```

上記のコード例の構造体は、Winspool.h で定義されます。

次のエスケープ コードは、Winddiui.h で定義されます。

```cpp
//
 // Escape code for XPS Document events
//
#define DOCUMENTEVENT_QUERYFILTER                                     14
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRE                 1
// DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRE must have same value as //DOCUMENTEVENT_CREATEDCPRE for Winspool.drv to query the driver for supported events and reset the cached events.
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPRE                         2
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPRE        3                           
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPOST                            4
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPOST                        5
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPOST                13
// DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPOST must have same value as //DOCUMENTEVENT_STARTDOCPOST for Winspool.drv to signal the tray ballon that //the document is completed
#define DOCUMENTEVENT_XPS_CANCELJOB                                   6
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPRE      7
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPRINTTICKETPRE              8
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPRINTTICKETPRE                  9
#define DOCUMENTEVENT_XPS_ADDFIXEDPAGEPRINTTICKETPOST                 10
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTPRINTTICKETPOST             11
#define DOCUMENTEVENT_XPS_ADDFIXEDDOCUMENTSEQUENCEPRINTTICKETPOST     12
```

 

 




