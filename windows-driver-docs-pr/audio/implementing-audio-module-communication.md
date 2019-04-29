---
title: オーディオ モジュール通信の実装
description: オーディオのモジュールは、distinct、オーディオ処理ロジックの比較的アトミックな関数を実行するのです。
ms.date: 07/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1c0705f6644d6413b77bd40e70cd10b9227f843
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333471"
---
<a name="implementing-audio-module-communication"></a>オーディオ モジュール通信の実装
========================================================================================

オーディオのモジュールは、distinct、オーディオ処理ロジックの比較的アトミックな関数を実行するのです。 オーディオのモジュールは、オーディオ ドライバーまたはオーディオ DSP に存在する可能性があります。 オーディオ モジュールの例は、オーディオ処理の DSP ベースになります。

1703 をリリース以降、Windows 10 では、Api と Ddi の両方からユニバーサル Windows プラットフォーム (UWP) アプリとカーネル モード デバイス ドライバーの通信をサポートするためには。

このトピックでは、カーネル デバイス ドライバーのオーディオ モジュール通信を実装する情報を提供します。 

コマンドを送信し、UWP アプリを使用してオーディオ デバイス モジュールからの変更通知を受信する方法については、次を参照してください。[とクエリの構成のオーディオ デバイス モジュール](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)します。

## <a name="why-use-audio-modules"></a>オーディオのモジュールを使用する理由

Oem は通常により、お客様はこのオーディオ システムの側面をコントロールにユーザーのシステム構成アプリケーションをバンドルし、優先順位を調整します。 オーディオのサブシステムは、ホスト上のオーディオ オブジェクト、ハードウェアの DSP 処理、および (すべてのオーディオ コーデック自体だけでなく) スマート amp などの特殊なハードウェアの処理などのさまざまなコンポーネントを含めることができます。 ほとんどの場合これらのコンポーネントが作成され、さまざまなベンダーが販売されています。 従来、Ihv は、プライベート Api を 1 つ別と統合し、個々 のコンポーネント間で情報の送信を作成しました。 既存の WIN32 アプリケーションが構成し、これらのプライベート Api を活用します。

[ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)広範なデバイス間で実行する 1 つのアプリケーションを有効にする Api のセットを提供します。 UWP には、新しいと外観を Windows 10 で実行されるアプリケーションの顧客の期待になったも導入されました。 非常に多くの Oem は、UWP のオーディオ設定アプリケーションをビルドするようです。 ただし、UWP (AppContainer サンド ボックス) のコア セキュリティ機能は、オーディオのサブシステムでは、その他のコンポーネントをアプリケーションからの通信を防止します。 これは、UWP でアクセスできない構成アプリで使用していたプライベート Api を表示します。 

1703 のリリース以降、Windows 10 では、オーディオ モジュールの UWP API は新しい KS プロパティ セットを探索可能である、カーネルおよびハードウェア層でのモジュールと通信するアプリケーションとユーザー モードのコンポーネントの構成を使用できます。
オーディオの IHV、Isv は、アプリケーションと Windows によって提供される、明確に定義されたインターフェイスを使用して、ハードウェア モジュールと通信できるサービスを記述できます。 オーディオ モジュール API の詳細については、次を参照してください[Windows.Media.Devices Namespace。](https://docs.microsoft.com/uwp/api/Windows.Media.Devices)


<a name="span-idaudiomoduledefinitionsspanaudio-module-definitions"></a><span id="Audio_Module_Definitions"></span>オーディオのモジュールの定義
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
これらの定義は、オーディオのモジュールに固有です。

用語 | 定義
------------ | -------------
オーディオのモジュール    | オーディオの処理ロジックの比較的アトミックな関数の実行の個別の一部。 オーディオ ドライバーまたはオーディオ DSP があります。 オーディオ モジュールの例は、オーディオ処理オブジェクト (APO) になります。


<a name="span-idcommondefinitionsspancommon-audio-definitions"></a><span id="Common_Definitions"></span>オーディオの一般的な定義
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
これらの定義は、通常、オーディオ ドライバーを使用する場合に使用されます。

用語 | 定義
------------ | -------------
OEM | Original Equipment Manufacturer (相手先ブランド供給)
IHV | 独立系ハードウェア ベンダー
ISV | 独立系ソフトウェア ベンダー
 |
HSA | ハードウェア サポートのアプリケーション
UWP | ユニバーサル Windows プラットフォーム
 | 
APO | オーディオ処理オブジェクト
DSP | デジタル信号処理

<a name="span-idarchitecturespanarchitecture"></a><span id="Architecture"></span>アーキテクチャ 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
オーディオのモジュールは、インプレース オーディオ コンポーネントのユーザー モードとカーネル モードの間でメッセージを送信する Windows のサポートされているメカニズムを配置します。 重要な違いは、オーディオのモジュールが、トランスポート パイプラインを標準化します。 そのトランスポート経由で通信プロトコルを確立しませんし、プロトコルを定義するには、Isv および ihv 向けに依存しています。 目的は、非常に小さな変更で、オーディオ モジュールを簡単に移行する既存のサード パーティ製の設計を許可します。

<Diagram Pending>

オーディオ モジュール API は、2 つの異なるターゲット方法、モジュールへのアクセスを提供します。、KS wave フィルターと初期化の KS pin (ストリーム)。 配置と特定のモジュールへのアクセスは、特定の実装です。

HSAs や他のアプリケーションはのみにアクセスできる使用可能なモジュール フィルター ハンドルを使用します。 ストリームに読み込まれる個々 の画像は、ストリームにアクセスできるオブジェクトのみがオーディオのモジュールを対象とします。

パスワードの詳細については、次を参照してください。 [Windows オーディオ処理オブジェクト](https://msdn.microsoft.com/windows/hardware/drivers/audio/windows-audio-processing-objects)します。

### <a name="sending-commands"></a>コマンドを送信します。

オーディオのサブシステムのカーネルとハードウェア コンポーネントでオーディオのモジュールにコマンドを送信するオーディオ モジュールのクライアントの手段をクエリおよびパラメーターを変更することです。 オーディオ モジュール API のコマンド構造は、広義し、モジュールが検出され、自身を識別する方法を形式化します。 ただし、詳細なコマンド構造に設計されています、関連する ISV および IHV のプロトコルをどのようなメッセージを送信できるを確立するために、想定される応答によって実装される必要があります。

### <a name="module-notifications-to-audio-module-clients"></a>オーディオのモジュールのクライアントに通知をモジュール

オーディオのミニポートに連絡して、クライアントは、特定のモジュールでの通知にサブスクライブしている場合は、オーディオのモジュールのクライアントに情報を渡す方法があります。 これらの通知に渡された情報は、オーディオ モジュール API によって定義されていないではなく、ISV および IHV によって定義されます。

### <a name="enable-disable-and-general-topology-information"></a>有効化、無効化、および一般的なトポロジの情報

オーディオ モジュール Api は、列挙、およびモジュールにコマンドを送信する方法を定義します。 ただし、Api は明示的に定義オーディオ モジュールのクライアントが有効にまたは特定のモジュールを無効にする方法。 また、クライアントがトポロジ情報または相互の関連モジュールの配置を検索するための方法は確立しません。 Ihv、Isv を調べるかどうかはこの機能が実装する方法を判断が必要です。

推奨される方法には、ドライバーのグローバル モジュールが公開します。 ドライバーのグローバル モジュールは、これらトポロジの特定の要求にカスタム コマンドを処理します。

<a name="span-idaudiomoduleddisspanaudio-module-ddis"></a><span id="Audio_Module_DDIs"></span>オーディオ モジュール Ddi
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
**オーディオのモジュールのプロパティをストリーミングするカーネル** 

新しい KS プロパティ セットで識別される[KSPROPSETID_AudioModule](https://msdn.microsoft.com/library/windows/hardware/mt808144(v=vs.85).aspx)、オーディオのモジュールに固有の 3 つのプロパティが定義されています。 

PortCls ミニポート ドライバーでは、直接ヘルパー インターフェイスが指定されていない各プロパティの応答を処理する必要があります。

#### <a name="ksmediah"></a>ksmedia.h:

``` C++
#define STATIC_KSPROPSETID_AudioModule \
    0xc034fdb0, 0xff75, 0x47c8, 0xaa, 0x3c, 0xee, 0x46, 0x71, 0x6b, 0x50, 0xc6
DEFINE_GUIDSTRUCT("C034FDB0-FF75-47C8-AA3C-EE46716B50C6", KSPROPSETID_AudioModule);
#define KSPROPSETID_AudioModule DEFINE_GUIDNAMED(KSPROPSETID_AudioModule)

typedef enum {
    KSPROPERTY_AUDIOMODULE_DESCRIPTORS            = 1,  
    KSPROPERTY_AUDIOMODULE_COMMAND                = 2,
    KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID = 3,
} KSPROPERTY_AUDIOMODULE;
```

### <a name="audio-module-descriptors"></a>オーディオ モジュール記述子

サポート、 [KSPROPERTY_AUDIOMODULE_DESCRIPTORS](https://msdn.microsoft.com/library/windows/hardware/mt808142(v=vs.85).aspx)プロパティとして、オーディオのモジュールが認識されているドライバーを識別します。 フィルターまたは暗証番号 (pin) のハンドルを使用してクエリを実行する、プロパティと、KSPROPERTY、DeviceIoControl の呼び出しの入力バッファーとして渡されます。 [KSAUDIOMODULE_DESCRIPTOR](https://msdn.microsoft.com/library/windows/hardware/mt808137(v=vs.85).aspx)が定義されているオーディオ ハードウェア内で各モジュールについて説明します。 これらの記述子の配列は、この要求に応答で返される

#### <a name="ksmediah"></a>ksmedia.h:

``` C++
#define AUDIOMODULE_MAX_NAME_SIZE 128

typedef struct _KSAUDIOMODULE_DESCRIPTOR
{
    GUID    ClassId; 
    ULONG   InstanceId;
    ULONG   VersionMajor;
    ULONG   VersionMinor;
    WCHAR   Name[AUDIOMODULE_MAX_NAME_SIZE];
} KSAUDIOMODULE_DESCRIPTOR, *PKSAUDIOMODULE_DESCRIPTOR;
```
詳細については、次を参照してください。 [KSAUDIOMODULE_DESCRIPTOR](https://msdn.microsoft.com/library/windows/hardware/mt808137(v=vs.85).aspx)します。

### <a name="audio-module-command"></a>オーディオのモジュールのコマンド

サポート、 [KSPROPERTY_AUDIOMODULE_COMMAND](https://msdn.microsoft.com/library/windows/hardware/mt808141(v=vs.85).aspx)プロパティは、クエリを実行して、オーディオのモジュールのパラメーターを設定するカスタム コマンドを送信するオーディオ モジュールのクライアントを使用します。 プロパティは、フィルターまたは暗証番号 (pin) のハンドルを使用して送信できる、 [KSAUDIOMODULE_PROPERTY](https://msdn.microsoft.com/library/windows/hardware/mt808139(v=vs.85).aspx) DeviceIoControl の呼び出しの入力バッファーとして渡されます。 クライアントできます必要に応じて追加情報を送信する隣接、 [KSAUDIOMODULE_PROPERTY](https://msdn.microsoft.com/library/windows/hardware/mt808139(v=vs.85).aspx)カスタム コマンドを送信する入力バッファーにします。

#### <a name="ksmediah"></a>ksmedia.h:

``` C++
#define AUDIOMODULE_MAX_DATA_SIZE 64000

typedef struct _KSPAUDIOMODULE_PROPERTY
{
    KSPROPERTY Property;
    GUID       ClassId;
    ULONG      InstanceId;
} KSAUDIOMODULE_PROPERTY, *PKSPAUDIOMODULE_PROPERTY;

```
詳細については、次を参照してください。 [KSAUDIOMODULE_PROPERTY](https://msdn.microsoft.com/library/windows/hardware/mt808139(v=vs.85).aspx)します。


### <a name="audio-module-notification-device-id"></a>オーディオ モジュール通知デバイスの ID

サポート、 [KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID](https://msdn.microsoft.com/library/windows/hardware/mt808143(v=vs.85).aspx)ミニポート シグナル通知を有効にして、オーディオのモジュールのクライアントに情報を渡すに必要です。 この ID の有効期間が公開されていると、Windows オーディオ スタックをアクティブにされているオーディオ デバイスの有効期間に関連付けられています。 フィルターまたは暗証番号 (pin) のハンドルを使用して、プロパティを送信することができます、KSPROPERTY が DeviceIoControl の呼び出しの入力バッファーとして渡されます。

詳細については、次を参照してください。 [KSAUDIOMODULE_PROPERTY](https://msdn.microsoft.com/library/windows/hardware/mt808139(v=vs.85).aspx)します。


<a name="span-idportclshelperspanportcls-helper---audio-module-notifications"></a><span id="PortCls_Helper"></span>PortCls ヘルパー - オーディオ モジュールの通知
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 オーディオのモジュールのクライアントに通知を送信するドライバー開発者を支援するために、新しいポートのインターフェイスが追加されました。 

#### <a name="portclsh"></a>PortCls.h:

``` C++
typedef struct _PCNOTIFICATION_BUFFER 
{
    UCHAR NotificationBuffer[1];
} PCNOTIFICATION_BUFFER, *PPCNOTIFICATION_BUFFER;

DECLARE_INTERFACE_(IPortClsNotifications,IUnknown)
{
    DEFINE_ABSTRACT_UNKNOWN()   // For IUnknown

    STDMETHOD_(NTSTATUS, AllocNotificationBuffer)
    (   THIS_
        _In_    POOL_TYPE       PoolType,
        _In_    USHORT          NumberOfBytes,
        _Out_   PPCNOTIFICATION_BUFFER* NotificationBuffer
    )   PURE;
    
    STDMETHOD_(void, FreeNotificationBuffer)
    (   THIS_
        _In_    PPCNOTIFICATION_BUFFER NotificationBuffer
    )   PURE;
    
    STDMETHOD_(void, SendNotificationBuffer)
    (   THIS_
        _In_    const GUID*     NotificationId,
        _In_    PPCNOTIFICATION_BUFFER NotificationBuffer
    )   PURE;
};

//
// Audio module notification definitions.
//
#define STATIC_KSNOTIFICATIONID_AudioModule \
    0x9C2220F0, 0xD9A6, 0x4D5C, 0xA0, 0x36, 0x57, 0x38, 0x57, 0xFD, 0x50, 0xD2
DEFINE_GUIDSTRUCT("9C2220F0-D9A6-4D5C-A036-573857FD50D2", KSNOTIFICATIONID_AudioModule);
#define KSNOTIFICATIONID_AudioModule DEFINE_GUIDNAMED(KSNOTIFICATIONID_AudioModule)

typedef struct _KSAUDIOMODULE_NOTIFICATION {
    union {
        struct {
            GUID        DeviceId;
            GUID        ClassId;
            ULONG       InstanceId;
            ULONG       Reserved;
        } ProviderId;
        LONGLONG        Alignment;
    };
} KSAUDIOMODULE_NOTIFICATION, *PKSAUDIOMODULE_NOTIFICATION;


```
詳しくは、次のトピックをご覧ください。

 [IPortClsNotifications](https://msdn.microsoft.com/library/windows/hardware/mt808133(v=vs.85).aspx)
    
 [IPortClsNotifications::AllocNotificationBuffer](https://msdn.microsoft.com/library/windows/hardware/mt808134(v=vs.85).aspx)

 [IPortClsNotifications::FreeNotificationBuffer](https://msdn.microsoft.com/library/windows/hardware/mt808135(v=vs.85).aspx)    
    
 [IPortClsNotifications::SendNotificationBuffer](https://msdn.microsoft.com/library/windows/hardware/mt808136(v=vs.85).aspx)    

### <a name="calling-sequence"></a>呼び出しシーケンス

そのポートを作成し、通知を送信するのには、ミニポートを呼び出します。  一般的な呼び出しシーケンスは、次の図に表示されます。

![AudioIPortClsNotifications の呼び出しシーケンス](images/AudioIPortClsNotificationsCallingSequenceDiagram.png)



 



