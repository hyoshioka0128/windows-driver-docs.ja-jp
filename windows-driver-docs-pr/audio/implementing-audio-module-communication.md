---
title: オーディオ モジュール通信の実装
description: オーディオモジュールは、比較的アトミックな関数を実行する、個別のオーディオ処理ロジックです。
ms.date: 07/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cda3dcefe3597ba6ffd5b2a10b051a435985b90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833252"
---
<a name="implementing-audio-module-communication"></a>オーディオ モジュール通信の実装
========================================================================================

オーディオモジュールは、比較的アトミックな関数を実行する、個別のオーディオ処理ロジックです。 オーディオモジュールは、オーディオドライバーまたはオーディオ DSP に存在する場合があります。 オーディオモジュールの例としては、DSP ベースのオーディオ処理があります。

Windows 10、リリース1703以降では、ユニバーサル Windows プラットフォーム (UWP) アプリおよびカーネルモードデバイスドライバーからの通信をサポートする Api と DDIs の両方が用意されています。

このトピックでは、カーネルデバイスドライバーでのオーディオモジュール通信の実装について説明します。 

UWP アプリを使用して、オーディオデバイスモジュールからコマンドを送信したり変更通知を受信したりする方法については、「[オーディオデバイスモジュールの構成とクエリ](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)」を参照してください。

## <a name="why-use-audio-modules"></a>オーディオモジュールを使用する理由

Oem は、通常、ユーザーがこのオーディオシステムの側面を制御し、好みに合わせて調整できるように、システムに構成アプリケーションをバンドルします。 オーディオサブシステムには、ホスト上のオーディオ処理オブジェクト、ハードウェア DSP 処理、スマート amp などの特殊なハードウェア (オーディオコーデック自体に加えて、すべて) などのさまざまなコンポーネントを含めることができます。 ほとんどの場合、これらのコンポーネントは異なるベンダーによって作成および販売されます。 これまで、Ihv は独自のプライベート Api を作成して相互に統合し、個々のコンポーネント間で情報を送信していました。 その後、既存の WIN32 構成アプリケーションは、これらのプライベート Api を活用します。

[ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)は、1つのアプリケーションを幅広いデバイスで実行できるようにする api のセットを提供します。 UWP では、Windows 10 で実行されているアプリケーションに対する顧客の期待になる新しいルックアンドフィールも導入されました。 多くの Oem は、UWP でオーディオ構成アプリケーションを構築したいと考えています。 ただし、UWP (AppContainer サンドボックス) のコアセキュリティ機能は、アプリケーションからオーディオサブシステム内の他のコンポーネントへの通信を防止します。 これにより、UWP では構成アプリによって使用されていたプライベート Api がレンダリングされます。 

Windows 10 リリース1703以降、Audio Modules UWP API を使用すると、構成アプリケーションとユーザーモードコンポーネントは、新しい KS プロパティセットを使用して検出可能なカーネルおよびハードウェアレイヤー内のモジュールと通信できます。
オーディオ IHV と Isv は、Windows によって提供される適切に定義されたインターフェイスを使用して、ハードウェアモジュールと通信できるアプリケーションやサービスを作成できます。 Audio modules API の詳細については、「 [Windows. Media. Devices 名前空間](https://docs.microsoft.com/uwp/api/Windows.Media.Devices)」を参照してください。


<a name="span-idaudio_module_definitionsspanaudio-module-definitions"></a><span id="Audio_Module_Definitions"></span>オーディオモジュール定義
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
これらの定義は、オーディオモジュールに固有のものです。

用語 | 定義
------------ | -------------
オーディオモジュール    | 比較的アトミックな関数を実行する、個別のオーディオ処理ロジック。 オーディオドライバーまたはオーディオ DSP に存在する可能性があります。 オーディオモジュールの例としては、オーディオ処理オブジェクト (APO) などがあります。


<a name="span-idcommon_definitionsspancommon-audio-definitions"></a><span id="Common_Definitions"></span>一般的なオーディオ定義
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
これらの定義は、通常、オーディオドライバーを操作するときに使用されます。

用語 | 定義
------------ | -------------
OEM | Original Equipment Manufacturer (相手先ブランド供給)
IHV | 独立系ハードウェアベンダー
ISV | 独立系ソフトウェアベンダー
 |
HSA | ハードウェアサポートアプリケーション
UWP | ユニバーサル Windows プラットフォーム
 | 
郵便局 | オーディオ処理オブジェクト
DSP | デジタル信号処理

<a name="span-idarchitecturespanarchitecture"></a><span id="Architecture"></span>構造 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
オーディオモジュールは、ユーザーモードとカーネルモードのオーディオコンポーネント間でメッセージを送信するために、Windows でサポートされているメカニズムを配置します。 重要な違いは、オーディオモジュールはトランスポートパイプラインを標準化することです。 このトランスポートでは通信プロトコルが確立されず、Isv と Ihv に依存してプロトコルが定義されます。 この目的は、既存のサードパーティ製のデザインを簡単にオーディオモジュールに移行できるようにすることです。変更はほとんどありません。

<Diagram Pending>

オーディオモジュール API は、2つの異なるターゲットメソッド (KS wave フィルターと初期化された KS pin (stream)) を介してモジュールにアクセスできるようにします。 特定のモジュールへの配置とアクセスは、実装固有のものです。

HSAs とその他のアプリケーションは、フィルターハンドルを通じて使用可能なモジュールにしかアクセスできません。 ストリームに読み込まれた個々の APOs は、ストリーム対象のオーディオモジュールにアクセスできる唯一のオブジェクトです。

APOs の詳細については、「 [Windows オーディオ処理オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/audio/windows-audio-processing-objects)」を参照してください。

### <a name="sending-commands"></a>コマンドの送信

オーディオモジュールクライアントがパラメーターを照会および変更するには、オーディオサブシステムのカーネルおよびハードウェアコンポーネントのオーディオモジュールにコマンドを送信します。 オーディオモジュール API のコマンド構造は、厳密に定義されており、モジュールの検出方法を形式化し、自身を識別します。 ただし、詳細なコマンドの構造は、関連する ISV と IHV によって設計および実装されている必要があります。これにより、送信できるメッセージと想定される応答のプロトコルが確立されます。

### <a name="module-notifications-to-audio-module-clients"></a>オーディオモジュールクライアントへのモジュール通知

また、オーディオミニポートには、クライアントが特定のモジュールで通知をサブスクライブしている場合に、オーディオモジュールクライアントに情報を通知して渡す方法もあります。 これらの通知で渡される情報は、音声モジュール API によって定義されるのではなく、ISV や IHV によって定義されます。

### <a name="enable-disable-and-general-topology-information"></a>有効化、無効化、および全般的なトポロジ情報

オーディオモジュール Api は、モジュールにコマンドを列挙して送信する方法を定義します。 ただし、Api では、オーディオモジュールクライアントが特定のモジュールを有効または無効にする方法が明示的に定義されていません。 また、クライアントがトポロジ情報や、相互に関連するモジュールの配置を検索する方法を確立することもありません。 Ihv および Isv は、この機能が必要かどうかを判断し、実装方法を決定できます。

グローバルドライバーモジュールを公開する方法をお勧めします。 グローバルドライバーモジュールは、これらのトポロジ固有の要求のカスタムコマンドを処理します。

<a name="span-idaudio_module_ddisspanaudio-module-ddis"></a><span id="Audio_Module_DDIs"></span>オーディオモジュール DDIs
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
**カーネルストリーミングオーディオモジュールのプロパティ** 

[KSPROPSETID_AudioModule](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audiomodule)によって識別される新しい KS プロパティセットが、オーディオモジュールに固有の3つのプロパティに対して定義されています。 

PortCls ミニポートドライバーは、ヘルパーインターフェイスが提供されていないため、各プロパティの応答を直接処理する必要があります。

#### <a name="ksmediah"></a>ksmedia. h:

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

### <a name="audio-module-descriptors"></a>オーディオモジュール記述子

[KSPROPERTY_AUDIOMODULE_DESCRIPTORS](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-descriptors)プロパティのサポートによって、オーディオモジュール対応としてドライバーが識別されます。 プロパティは、フィルターまたはピンハンドルを介してクエリされ、DeviceIoControl 呼び出しの入力バッファーとして KSK プロパティが渡されます。 [KSAUDIOMODULE_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)は、オーディオハードウェア内の各モジュールを記述するように定義されています。 この要求に応答して、これらの記述子の配列が返されます。

#### <a name="ksmediah"></a>ksmedia. h:

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
詳細については、「 [KSAUDIOMODULE_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)」を参照してください。

### <a name="audio-module-command"></a>オーディオモジュールコマンド

[KSPROPERTY_AUDIOMODULE_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-command)プロパティをサポートすることで、オーディオモジュールクライアントがカスタムコマンドを送信し、オーディオモジュールのパラメーターを照会および設定できるようになります。 プロパティは、フィルターまたはピンハンドルを介して送信できます。 [KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)は、DeviceIoControl 呼び出しの入力バッファーとして渡されます。 クライアントは、必要に応じて、入力バッファー内の[KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)に隣接する追加情報を送信して、カスタムコマンドを送信できます。

#### <a name="ksmediah"></a>ksmedia. h:

``` C++
#define AUDIOMODULE_MAX_DATA_SIZE 64000

typedef struct _KSPAUDIOMODULE_PROPERTY
{
    KSPROPERTY Property;
    GUID       ClassId;
    ULONG      InstanceId;
} KSAUDIOMODULE_PROPERTY, *PKSPAUDIOMODULE_PROPERTY;

```
詳細については、「 [KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)」を参照してください。


### <a name="audio-module-notification-device-id"></a>オーディオモジュール通知デバイス ID

ミニポートが通知に信号を送信し、オーディオモジュールクライアントに情報を渡すことができるようにするには、 [KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-notification-device-id)のサポートが必要です。 この ID の有効期間は、オーディオデバイスが公開され、Windows オーディオスタックに対してアクティブになっている有効期間に関連付けられています。 プロパティは、フィルターまたはピンハンドルを介して送信できます。また、DeviceIoControl 呼び出しの入力バッファーとして KSK プロパティが渡されます。

詳細については、「 [KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)」を参照してください。


<a name="span-idportcls_helperspanportcls-helper---audio-module-notifications"></a><span id="PortCls_Helper"></span>PortCls Helper-Audio モジュール通知
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 ドライバー開発者がオーディオモジュールクライアントに通知を送信できるように、新しいポートインターフェイスが追加されました。 

#### <a name="portclsh"></a>PortCls:

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

 [IPortClsNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsnotifications)
    
 [IPortClsNotifications:: AllocNotificationBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsnotifications-allocnotificationbuffer)

 [IPortClsNotifications:: FreeNotificationBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsnotifications-freenotificationbuffer)   
    
 [IPortClsNotifications:: SendNotificationBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsnotifications-sendnotification) 

### <a name="calling-sequence"></a>呼び出しシーケンス

ミニポートは、通知を作成して送信するために、ポートを呼び出します。  一般的な呼び出しシーケンスを次の図に示します。

![AudioIPortClsNotifications 呼び出しシーケンス](images/AudioIPortClsNotificationsCallingSequenceDiagram.png)



 



