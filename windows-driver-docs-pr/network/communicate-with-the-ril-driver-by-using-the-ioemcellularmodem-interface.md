---
title: IOemCellularModem インターフェイスを使用して、RIL ドライバーとの通信します。
description: このトピックでは、IOemCellularModem インターフェイスを使用して、RIL ドライバーと通信する方法について説明します。
ms.assetid: 612a7f98-053f-4447-bb0e-c6f34969df5d
keywords:
- IOemCellularModem インターフェイスのネットワーク ドライバーを使用して、RIL ドライバーとの通信します。
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c8b465ac667d458874a1fcd1346b06b5bd711c7
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136131"
---
# <a name="communicate-with-the-ril-driver-by-using-the-ioemcellularmodem-interface"></a>IOemCellularModem インターフェイスを使用して、RIL ドライバーとの通信します。

> [!WARNING]
> 携帯電話の COM API は、Windows 10 で非推奨とされます。 このコンテンツは、OEM および携帯電話会社が Windows Phone 8.1 アプリケーションの作成の保守をサポートするために提供されます。

使用することができます、 [IOemCellularModem](https://msdn.microsoft.com/library/windows/hardware/dn946687) OEM RIL ドライバーと通信するインターフェイス。 パートナーが使用できる場合は、制限付きのプラットフォームで Api を使用して、モデムとの通信には、(RPAL) ボックスの一覧。

携帯電話の COM Api の詳細については、[携帯電話の COM API リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn946508)を参照してください。

## <a name="using-cellular-com-apis"></a>携帯電話の COM Api を使用します。

携帯電話の COM Api を使用するへのポインターを取得、 [IOemCellular](https://msdn.microsoft.com/library/windows/hardware/dn946677)を呼び出してインスタンス**CoCreateInstanceFromApp**します。 呼び出し元アプリケーションには、使用するには IOemCellular インターフェイスへのポインターが必要な[IOemCellularModem](https://msdn.microsoft.com/library/windows/hardware/dn946687)インターフェイス。 

[IOemCellular::RegisterForOemModemExistenceChanges](https://msdn.microsoft.com/library/windows/hardware/dn931023)メソッドを使用して、モデムが一覧表示します。 メソッドが呼び出されると、 [IOemCellularModemExistenceChange::OnOemModemAdded](https://msdn.microsoft.com/library/windows/hardware/dn946689)が呼び出されると、 [IOemCellularModem](https://msdn.microsoft.com/library/windows/hardware/dn946687)ポインター。

このコードでは、取得、 [IOemCellular](https://msdn.microsoft.com/library/windows/hardware/dn946677)を使用してポインター **CoCreateInstanceFromApp**します。 CoCreateInstanceFromApp は、特定のインターフェイスを 1 つまたは複数のポインターを返すことができます。 必要なインターフェイスは、クエリ [0] .pIID によって指定される、IOemCellular です。 OemCellular は、サポートする COM クラス; への参照クラスをアクティブにするファクトリを決定します。 

```c++
    MULTI_QI query[1];
    query[0].pIID = &__uuidof(IOemCellular);
    query[0].pItf = nullptr;
    query[0].hr = S_OK;

    hr = CoCreateInstanceFromApp(__uuidof(OemCellular), nullptr, CLSCTX_INPROC_SERVER,
                                nullptr, _countof(query), query);
    ...
```
このコードへのポインターを登録するかを示しています。 [IOemCellularModemExistenceChange](https://msdn.microsoft.com/library/windows/hardware/dn946688)を使用して[IOemCellular::RegisterForOemModemExistenceChanges](https://msdn.microsoft.com/library/windows/hardware/dn931023)します。 次のコードではへのポインター **CModems** IOemCellularModemExistenceChange インターフェイスを提供します。

```c++
    HRESULT hr;
    hr = m_spCellular->RegisterForOemModemExistenceChanges(this);

    ...
```

このコードは、実装する方法を示しています。 **OnOemModemAdded**やの他のメソッド、 [IOemCellularModemExistenceChange](https://msdn.microsoft.com/library/windows/hardware/dn946688)インターフェイス。

```c++
class CModems : public IOemCellularModemExistenceChange, public CellBase
{
    ...

    // 
    // IOemCellularModemExistenceChange interface
    //
    IFACEMETHOD(OnOemModemAdded)(IOemCellularModem *pModem);
    IFACEMETHOD(OnOemModemRemoved)(IOemCellularModem *pModem);
    IFACEMETHOD(OnOemModemExistenceDone)();

    ...
};
IFACEMETHODIMP CModems::OnOemModemAdded(IOemCellularModem *pModem)
{
    ComPtr<IOemCellularModem> spModem(pModem);
    m_ModemList.push_back(spModem);
    return S_OK;
}
```

## <a name="sending-opaque-data-to-ril"></a>RIL を非透過データを送信します。

表示されたら、 **IOemCellularModem**を呼び出すことによってポインター **OnOemModemAdded**、 [IOemCellularModem::SendModemOpaqueCommand](https://msdn.microsoft.com/library/windows/hardware/dn931017)ことができます。 Cellcore を呼び出し、バック グラウンドで、 **RIL_DevSpecific**渡されたパラメーターを持つ関数です。 RIL ドライバーでは、この要求を処理し、上位の層への応答を送信します。 応答が配信された後、コールバックを[IModemOpaqueCommandCompletion::OnModemOpaqueCommandCompletion](https://msdn.microsoft.com/library/windows/hardware/dn946648)の結果とが呼び出される、 **SendModemOpaqueCommand**呼び出します。

このコードでは非透過的なデータに送信、 [IOemCellularModem::SendModemOpaqueCommand](https://msdn.microsoft.com/library/windows/hardware/dn931017)します。

```c++
    void CCellcoreComponent::CAgent::SetRadioPowerState(bool fPowerOn)
    {
        DWORD command[2];
        command[0] = CMD_SET_EQUIPMENTSTATE;
        command[1] = fPowerOn ? RIL_EQSTATE_FULL : RIL_EQSTATE_MINIMUM;
        m_spModem->SendModemOpaqueCommand(this, (BYTE*)command, sizeof(command), 
            (INT_PTR) CMD_SET_EQUIPMENTSTATE);
    ...
```

前のコード例では、コマンドは、無線をオンまたはオフにするために RIL に送信されます。 RIL ドライバーを 2 つの DWORD データ要素を処理するために設計するときに**RIL_DevSpecific**が呼び出されます。 独自の構造と、ニーズに合わせてコマンドを定義することができます。 応答は、完了コールバックし、コマンドの完了後、RIL ドライバーを送信します ([IModemOpaqueCommandCompletion::OnModemOpaqueCommandCompletion](https://msdn.microsoft.com/library/windows/hardware/dn946648)) が呼び出されます。 

このコードでは、受信側の完了イベントを処理、 **SendModemOpaqueCommand**前の例ではコマンド。

```c++
IFACEMETHODIMP CCellcoreComponent::CAgent::OnModemOpaqueCommandCompletion (
            /* [in] */ HRESULT result,
            /* [size_is][in] */ BYTE *pOpaqueResponse,
            /* [in] */ DWORD cbSize,
            /* [in] */ INT_PTR context)
{
    if (SUCCEEDED(result))
    {
        if ((int)context == CMD_SET_EQUIPMENTSTATE)
        {
            //
            // add routine if it is necessary to handle completion.
            //
        }
    }

    return S_OK;
}
```

> [!NOTE]
> **要求、応答、および通知の最大サイズ**-The RIL アダプテーション層は RIL コマンド、応答、および通知のペイロードの 0x2800 (10240) バイトの最大サイズの制約を適用します。 このサイズには、致命的なエラーが発生しより大きなペイロード。

## <a name="receiving-a-notification-from-ril"></a>RIL から通知を受け取る

携帯電話のインターフェイスで始まる RIL 通知のいくつか提供されます**RIL_NOTIFY**と同様に、 **RIL_NOTIFY_SIGNALQUALITY**します。 **IOemCellularModem** RIL 通知を受信する既定の方法を提供しません。 1 つのオプションは、使用する[IOemCellularModem::RegisterForOpaqueModemNotifications](https://msdn.microsoft.com/library/windows/hardware/dn931015)のこれらの OEM RIL 通知します。 これを行うには、独自の RIL 通知メッセージをまず定義より小さい**RIL_NOTIFY_OEM_MAX**RilAPITypes.h で定義されています。 RIL、OEM RIL 通知を送信するたびに[IOpaqueModemNotifications::OnOpaqueModemNotifications](https://msdn.microsoft.com/library/windows/hardware/dn931072)コールバック ポインターが IOemCellularModem::RegisterForOpaqueModemNotifications によって登録された後に呼び出されます。 

このコードを呼び出す方法を示します[IOemCellularModem::RegisterForOpaqueModemNotifications](https://msdn.microsoft.com/library/windows/hardware/dn931015)します。

```c++
HRESULT CCellcoreComponent::CAgent::Initialize()
{
    ...
    IFFAILED_EXIT(m_spModem->RegisterForOpaqueModemNotifications(this));
    ...
```

このコードは、実装する方法を示しています。 [IOpaqueModemNotifications::OnOpaqueModemNotifications](https://msdn.microsoft.com/library/windows/hardware/dn931072)します。 コードには、信号のバーの数を返す通知コールバック ハンドルが含まれています。 呼び出し元のアプリケーションの両方を RIL ドライバーでは、カスタム定義通知 RIL_NOTIFY_OEM_SIGNALSTRENGTH を実装する必要があります。

```c++
class CAgent : 
        public IOpaqueModemNotifications, 
        public IModemOpaqueCommandCompletion,
        public IPowerStateChange,
        public IPositionInfoCompletion,
        public IAgent
{
    ...

    //
    // IOpaqueModemNotifications
    //
    IFACEMETHOD(OnOpaqueModemNotifications)( 
    /* [in] */ DWORD dwCode,
    /* [in] */ BYTE *pOpaqueNotification,
    /* [in] */ DWORD cbSize);

                }
IFACEMETHODIMP CCellcoreComponent::CAgent::OnOpaqueModemNotifications( 
            /* [in] */ DWORD dwCode,
            /* [in] */ BYTE *pOpaqueNotification,
            /* [in] */ DWORD cbSize)
{
    wchar_t szResultString[STRING_BUF_LEN] = {0,};

    // check dwCode to fill notification result string.
    if (dwCode == RIL_NOTIFY_OEM_SIGNALSTRENGTH)
    {
        DWORD dwSignalBar;
        if (cbSize == sizeof(DWORD))
        {
            dwSignalBar = *((DWORD*)pOpaqueNotification);
        }
        else
        {
            dwSignalBar = -1;
        }

        swprintf_s(szResultString, STRING_BUF_LEN, L"Num of signal bars : %d", dwSignalBar );
    }
    else
    {
        swprintf_s(szResultString, STRING_BUF_LEN, L"Unknown Notification");
    }

    // send notification string.
    String ^ opaqueInfo = ref new String (szResultString);
    m_cellcore->OnOpaqueNotification(opaqueInfo);

    return S_OK;
}
```

## <a name="related-topics"></a>関連トピック

[携帯電話の COM API の設計ガイド](cellular-com-api-design-guide.md)

[携帯電話の COM API リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn946508)

