---
Description: このトピックには、WinUSB 関数を使用して、関数ドライバーとして Winusb.sys を使用している USB デバイスと通信する方法について詳細なチュートリアルが含まれています。
title: WinUSB 関数を使用して USB デバイスにアクセスする方法
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 214dfc6d36eef05f533aa4eed749ef1a998d1bc8
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79437067"
---
# <a name="how-to-access-a-usb-device-by-using-winusb-functions"></a>WinUSB 関数を使用して USB デバイスにアクセスする方法


**要約**

-   デバイスを開いて WinUSB ハンドルを取得します。
-   すべてのインターフェイスとそれらのエンドポイントのデバイス、構成、およびインターフェイスの設定に関する情報を取得します。
-   バルクに対するデータの読み取りと書き込みを行い、エンドポイントを中断します。

**重要な API**

-   [SetupAPI 関数](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)
-   [WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)

このトピックには、[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を使用して、関数ドライバーとして Winusb.sys を使用している USB デバイスと通信する方法について詳細なチュートリアルが含まれています。

Microsoft Visual Studio 2013 を使用している場合は、WinUSB テンプレートを使用してスケルトン アプリを作成します。 その場合は、このトピックの手順 1 - 3 をスキップし、手順 4 から続行します。 このテンプレートは、デバイスへのファイル ハンドルを開き、以降の操作に必要な WinUSB ハンドルを取得します。 そのハンドルは、device.h 内のアプリ定義の DEVICE\_DATA 構造体に格納されます。

テンプレートの詳細については、「WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する」を参照してください。

**注**  WinUSB 関数には、Windows XP 以降が必要です。 これらの関数を C/C++ アプリケーションで使用して、USB デバイスと通信することができます。 Microsoft は WinUSB 用のマネージ API を提供していません。

## <a name="prerequisites"></a><a href="" id="pre"></a>前提条件


このチュートリアルには、次の項目が適用されます。

-   この情報は、Windows 8.1、Windows 8、Windows 7、Windows Server 2008、Windows Vista の各 Windows バージョンに適用されます。
-   デバイスの関数ドライバーとして Winusb.sys をインストールしている必要があります。 このプロセスの詳細については、「[WinUSB (Winusb.sys) のインストール](winusb-installation.md)」を参照してください。
-   このトピックの例は、[OSR USB FX2 Learning Kit デバイス](https://www.osronline.com/)に基づいています。 これらの例を使用して、手順を他の USB デバイスに拡張できます。

## <a name="step-1-create-a-skeleton-app-based-on-the-winusb-template"></a><a href="" id="setup"></a>手順 1: WinUSB テンプレートに基づいてスケルトン アプリを作成する


USB デバイスにアクセスするには、まず、Windows Driver Kit (WDK) と Microsoft Visual Studio の統合環境 (Debugging Tools for Windows を含む) に含まれる WinUSB テンプレートに基づいてスケルトン アプリを作成します。

テンプレート コードの詳細と、スケルトン アプリを作成、ビルド、デプロイ、およびデバッグする方法の詳細については、「[WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)」を参照してください。

このテンプレートは、[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi) ルーチンを使用してデバイスを列挙し、デバイスのファイル ハンドルを開いて、以降のタスクに必要な WinUSB インターフェイス ハンドルを作成します。 デバイス ハンドルを取得してデバイスを開くコード例については、[テンプレート コードの説明](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)に関するページを参照してください。

## <a name="step-2-query-the-device-for-usb-descriptors"></a><a href="" id="query"></a>手順 2: デバイスに USB 記述子を照会する


次に、デバイスに USB 固有の情報 (デバイスの速度、インターフェイス記述子、関連するエンドポイント、そのパイプなど) を照会します。 この手順は、USB デバイス ドライバーが使用する手順とよく似ています。 ただし、アプリケーションは、[**WinUsb\_GetDescriptor**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor) を呼び出してデバイス クエリを実行します。

次の一覧は、USB 固有の情報を取得するために呼び出すことができる WinUSB 関数を示します。

-   追加のデバイス情報。

    デバイスのデバイス記述子の情報を要求するには、[**WinUsb\_QueryDeviceInformation**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querydeviceinformation) を呼び出します。 デバイスの速度を取得するには、*InformationType* パラメーターに DEVICE\_SPEED (0x01) を設定します。 関数は、LowSpeed (0x01) または HighSpeed (0x03) を返します。

-   インターフェイス記述子

    対応するインターフェイス記述子を取得するには、[**WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings) を呼び出して、デバイスのインターフェイス ハンドルを渡します。 WinUSB インターフェイス ハンドルは、最初のインターフェイスに対応します。 OSR Fx2 デバイスなどの一部の USB デバイスでは、1 つのインターフェイスのみをサポートし、代替設定は使用されません。 このため、これらのデバイスの場合、*AlternateSettingNumber* パラメーターを 0 に設定し、関数を 1 回だけ呼び出します。 **WinUsb\_QueryInterfaceSettings** は、呼び出し元で割り当てられた [**USB\_INTERFACE\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor) 構造体 (*UsbAltInterfaceDescriptor* パラメーターで渡された) にインターフェイスに関する情報を設定します。 たとえば、インターフェイス内のエンドポイント数は、**USB\_INTERFACE\_DESCRIPTOR** の **bNumEndpoints** メンバーで設定されます。

    複数のインターフェイスをサポートするデバイスの場合は、*AssociatedInterfaceIndex* パラメーターで代替設定を指定して [**WinUsb\_GetAssociatedInterface**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface) を呼び出すことで、関連付けられたインターフェイスのインターフェイス ハンドルを取得します。

-   エンドポイント

    各インターフェイスの各エンドポイントに関する情報を取得するには、[**WinUsb\_QueryPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe) を呼び出します。 **WinUsb\_QueryPipe** は、呼び出し元で割り当てられた [**WINUSB\_PIPE\_INFORMATION**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information) 構造体に、指定されたエンドポイントのパイプに関する情報を設定します。 エンドポイントのパイプは、0 から始まるインデックスによって識別されます。また、[**WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings) への以前の呼び出しで取得されたインターフェイス記述子の **bNumEndpoints** メンバーの値より小さい値である必要があります。 OSR Fx2 デバイスには、3 つのエンドポイントを持つインターフェイスが 1 つあります。 このデバイスの場合、関数の *AlternateInterfaceNumber* パラメーターは 0 に設定され、*PipeIndex* パラメーターの値は 0 から 2 の範囲で変化します。

    パイプの種類を特定するには、[**WINUSB\_PIPE\_INFORMATION**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information) 構造体の **PipeInfo** メンバーを調べます。 このメンバーは、[**USBD\_PIPE\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ne-usb-_usbd_pipe_type) 列挙値 (UsbdPipeTypeControl、UsbdPipeTypeIsochronous、UsbdPipeTypeBulk、または UsbdPipeTypeInterrupt) のいずれかに設定されます。 OSR USB FX2 デバイスは、割り込みパイプ、バルクイン パイプ、バルクアウト パイプをサポートするため、**PipeInfo** は、UsbdPipeTypeInterrupt または UsbdPipeTypeBulk のいずれかに設定されます。 UsbdPipeTypeBulk の値は、バルク パイプを識別しますが、パイプの方向を指定しません。 方向情報は、パイプ アドレスの上位ビットでエンコードされ、**WINUSB\_PIPE\_INFORMATION** 構造体の **PipeId** メンバーに格納されます。 パイプの方向を最も簡単に特定するには、**PipeId** の値を、Usb100.h から次のマクロのいずれかに渡します。

    -   方向がインの場合、`USB_ENDPOINT_DIRECTION_IN (PipeId)` マクロは **TRUE** を返します。
    -   方向がアウトの場合、`USB_ENDPOINT_DIRECTION_OUT(PipeId)` マクロは **TRUE** を返します。

    アプリケーションは、**PipeId** の値を使用して、[**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe) (このトピックの「I/O 要求を発行する」セクションを参照) などの WinUSB 関数への呼び出しでデータ転送に使用するパイプを識別するため、この例では、後で使用するために、**PipeId** の 3 つの値をすべて格納します。

次のコード例では、WinUSB インターフェイス ハンドルで指定されたデバイスの速度を取得します。

```ManagedCPlusPlus
BOOL GetUSBDeviceSpeed(WINUSB_INTERFACE_HANDLE hDeviceHandle, UCHAR* pDeviceSpeed)
{
    if (!pDeviceSpeed || hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    ULONG length = sizeof(UCHAR);

    bResult = WinUsb_QueryDeviceInformation(hDeviceHandle, DEVICE_SPEED, &length, pDeviceSpeed);
    if(!bResult)
    {
        printf("Error getting device speed: %d.\n", GetLastError());
        goto done;
    }

    if(*pDeviceSpeed == LowSpeed)
    {
        printf("Device speed: %d (Low speed).\n", *pDeviceSpeed);
        goto done;
    }
    if(*pDeviceSpeed == FullSpeed)
    {
        printf("Device speed: %d (Full speed).\n", *pDeviceSpeed);
        goto done;
    }
    if(*pDeviceSpeed == HighSpeed)
    {
        printf("Device speed: %d (High speed).\n", *pDeviceSpeed);
        goto done;
    }

done:
    return bResult;
}
```

次のコード例では、WinUSB インターフェイス ハンドルで指定された USB デバイスのさまざまな記述子を照会します。 この例の関数は、サポートされるエンドポイントの種類とそのパイプ識別子を取得します。 この例では、後で使用するために、3 つの PipeId 値をすべて格納します。

```ManagedCPlusPlus
struct PIPE_ID
{
    UCHAR  PipeInId;
    UCHAR  PipeOutId;
};

BOOL QueryDeviceEndpoints (WINUSB_INTERFACE_HANDLE hDeviceHandle, PIPE_ID* pipeid)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    USB_INTERFACE_DESCRIPTOR InterfaceDescriptor;
    ZeroMemory(&InterfaceDescriptor, sizeof(USB_INTERFACE_DESCRIPTOR));

    WINUSB_PIPE_INFORMATION  Pipe;
    ZeroMemory(&Pipe, sizeof(WINUSB_PIPE_INFORMATION));

    
    bResult = WinUsb_QueryInterfaceSettings(hDeviceHandle, 0, &InterfaceDescriptor);

    if (bResult)
    {
        for (int index = 0; index < InterfaceDescriptor.bNumEndpoints; index++)
        {
            bResult = WinUsb_QueryPipe(hDeviceHandle, 0, index, &Pipe);

            if (bResult)
            {
                if (Pipe.PipeType == UsbdPipeTypeControl)
                {
                    printf("Endpoint index: %d Pipe type: Control Pipe ID: %d.\n", index, Pipe.PipeType, Pipe.PipeId);
                }
                if (Pipe.PipeType == UsbdPipeTypeIsochronous)
                {
                    printf("Endpoint index: %d Pipe type: Isochronous Pipe ID: %d.\n", index, Pipe.PipeType, Pipe.PipeId);
                }
                if (Pipe.PipeType == UsbdPipeTypeBulk)
                {
                    if (USB_ENDPOINT_DIRECTION_IN(Pipe.PipeId))
                    {
                        printf("Endpoint index: %d Pipe type: Bulk Pipe ID: %c.\n", index, Pipe.PipeType, Pipe.PipeId);
                        pipeid->PipeInId = Pipe.PipeId;
                    }
                    if (USB_ENDPOINT_DIRECTION_OUT(Pipe.PipeId))
                    {
                        printf("Endpoint index: %d Pipe type: Bulk Pipe ID: %c.\n", index, Pipe.PipeType, Pipe.PipeId);
                        pipeid->PipeOutId = Pipe.PipeId;
                    }

                }
                if (Pipe.PipeType == UsbdPipeTypeInterrupt)
                {
                    printf("Endpoint index: %d Pipe type: Interrupt Pipe ID: %d.\n", index, Pipe.PipeType, Pipe.PipeId);
                }
            }
            else
            {
                continue;
            }
        }
    }

done:
    return bResult;
}
```

## <a name="step-3-send-control-transfer-to-the-default-endpoint"></a><a href="" id="control"></a>手順 3: 既定のエンドポイントにコントロール転送を送信する


次に、既定のエンドポイントに制御要求を発行してデバイスと通信します。

すべての USB デバイスには、インターフェイスと関連付けられているエンドポイントに加えて、既定のエンドポイントがあります。 既定のエンドポイントの主な目的は、デバイスの構成に使用できる情報をホストに提供することです。 ただし、デバイスは、デバイス固有の目的で既定のエンドポイントを使用することもできます。 たとえば、OSR USB FX2 デバイスは既定のエンドポイントを使用して、ライト バーと 7 セグメント デジタル ディスプレイを制御します。

制御コマンドは、8 バイトのセットアップ パケットで構成されます。これには、特定の要求を指定する要求コードとオプションのデータ バッファーが含まれます。 要求コードとバッファー形式は、ベンダーで定義されます。 この例のアプリケーションは、データをデバイスに送信して、ライト バーを制御します。 ライト バーを設定するコードは 0xD8 です。これは、便宜上、SET\_BARGRAPH\_DISPLAY として定義されます。 この要求の場合、デバイスには、適切なビットを設定して、どの要素を点灯する必要があるかを指定する 1 バイトのデータ バッファーが必要です。

アプリケーションでは、ユーザー インターフェイス (UI) を使用してこれを設定できます。たとえば、ライト バーのどの要素を点灯する必要があるかを指定する 8 個のチェック ボックス コントロール セットを提供します。 指定された要素は、バッファー内の適切なビットに対応します。 UI コードを回避するために、このセクションのコード例では、ライトが交互に点灯するようにビットを設定します。

**制御要求を発行するには、次の手順を使用します。**

1.  1 バイトのデータ バッファーを割り当てて、適切なビットを設定して点灯する必要がある要素を指定するバッファーにデータを読み込みます。
2.  呼び出し元で割り当てられた [**WINUSB\_SETUP\_PACKET**](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet) 構造体にセットアップ パケットを構築します。 要求の種類とデータを表すメンバーを次のように初期化します。
    -   **RequestType** メンバーは、要求の方向を指定します。 これを、ホストからデバイスへのデータ転送を示す 0 に設定します。 デバイスからホストへの転送の場合は、RequestType を 1 に設定します。
    -   **Request** メンバーを、この要求のベンダー定義コードである 0xD8 に設定します。 これは、便宜上、SET\_BARGRAPH\_DISPLAY として定義されます。
    -   **Length** メンバーを、データ バッファーのサイズに設定します。
    -   この要求では、**Index** メンバーと **Value** メンバーは必要ないため、0 に設定します。

3.  [**WinUsb\_ControlTransfer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer) を呼び出して、デバイスの WinUSB インターフェイス ハンドル、セットアップ パケット、データ バッファーを渡すことにより、既定のエンドポイントに要求を送信します。 関数は、*LengthTransferred* パラメーターで、デバイスに転送されたバイト数を受け取ります。

次のコード例は、指定された USB デバイスに制御要求を送信して、ライト バーのライトを制御します。

```ManagedCPlusPlus
BOOL SendDatatoDefaultEndpoint(WINUSB_INTERFACE_HANDLE hDeviceHandle)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    
    UCHAR bars = 0;

    WINUSB_SETUP_PACKET SetupPacket;
    ZeroMemory(&SetupPacket, sizeof(WINUSB_SETUP_PACKET));
    ULONG cbSent = 0;

    //Set bits to light alternate bars
    for (short i = 0; i < 7; i+= 2)
    {
        bars += 1 << i;
    }

    //Create the setup packet
    SetupPacket.RequestType = 0;
    SetupPacket.Request = 0xD8;
    SetupPacket.Value = 0;
    SetupPacket.Index = 0; 
    SetupPacket.Length = sizeof(UCHAR);

    bResult = WinUsb_ControlTransfer(hDeviceHandle, SetupPacket, &bars, sizeof(UCHAR), &cbSent, 0);
    if(!bResult)
    {
        goto done;
    }

    printf("Data sent: %d \nActual data transferred: %d.\n", sizeof(bars), cbSent);


done:
    return bResult;

}
```

## <a name="step-4-issue-io-requests"></a><a href="" id="io"></a>手順 4: I/O 要求を発行する


次に、データをデバイスのバルクイン エンドポイントとバルクアウト エンドポイントに送信します。これらはそれぞれ、要求の読み取りと書き込みに使用できます。 OSR USB FX2 デバイスでは、これらの 2 つのエンドポイントは、ループバック用に構成されるため、デバイスはデータをバルクイン エンドポイントからバルクアウト エンドポイントに移動します。 これにより、データの値が変更されたり、新しいデータが追加されたりすることはありません。 ループバック構成の場合、読み取り要求は、最新の書き込み要求で送信されたデータを読み取ります。 WinUSB には、書き込み要求と読み取り要求を送信するための次の関数が用意されています。

-   [**WinUsb\_WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)
-   [**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)

**書き込み要求の送信**

1.  バッファーを割り当てて、デバイスに書き込むデータをそれに格納します。 アプリケーションでパイプのポリシーの種類として RAW\_IO が設定されない場合、バッファーのサイズに制限はありません。 WinUSB は、必要に応じて、バッファーを適切なサイズのチャンクに分割します。 RAW\_IO が設定されている場合、バッファーのサイズは、WinUSB でサポートされる最大転送サイズによって制限されます。
2.  [**WinUsb\_WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe) を呼び出して、バッファーをデバイスに書き込みます。 デバイスの WinUSB インターフェイス ハンドル、バルクアウト パイプのパイプ識別子 (このトピックの「[デバイスに USB 記述子を照会する](#query)」セクションを参照)、およびバッファーを渡します。 関数は、*bytesWritten* パラメーターで、デバイスに実際に書き込まれたバイト数を返します。 *Overlapped* パラメーターを **NULL** に設定して、同期操作を要求します。 非同期の書き込み要求を実行するには、*Overlapped* を、**OVERLAPPED** 構造体を指すポインターに設定します。

長さゼロのデータを含む書き込み要求は、USB スタックに転送されます。 転送の長さが、転送の最大長を超える場合、WinUSB は要求を、転送の最大長より小さい要求に分割して、それを順に送信します。
次のコード例は、文字列を割り当てて、それをデバイスのバルクアウト エンドポイントに送信します。

```ManagedCPlusPlus
BOOL WriteToBulkEndpoint(WINUSB_INTERFACE_HANDLE hDeviceHandle, UCHAR* pID, ULONG* pcbWritten)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE || !pID || !pcbWritten)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    UCHAR szBuffer[] = "Hello World";
    ULONG cbSize = strlen(szBuffer);
    ULONG cbSent = 0;

    bResult = WinUsb_WritePipe(hDeviceHandle, *pID, szBuffer, cbSize, &cbSent, 0);
    if(!bResult)
    {
        goto done;
    }

    printf("Wrote to pipe %d: %s \nActual data transferred: %d.\n", *pID, szBuffer, cbSent);
    *pcbWritten = cbSent;


done:
    return bResult;

}
```

**読み取り要求の送信**

-   [**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe) を呼び出して、デバイスのバルクイン エンドポイントからデータを読み取ります。 デバイスの WinUSB インターフェイス ハンドル、バルクイン エンドポイントのパイプ識別子、および適切なサイズの空のバッファーを渡します。 関数が戻ると、バッファーには、デバイスから読み取られたデータが格納されています。 読み取られたバイト数は、関数の *bytesRead* パラメーターで返されます。 読み取り要求の場合、バッファーは、最大パケット サイズの倍数である必要があります。

長さゼロの読み取り要求は、正常に終了するとすぐに終了し、スタックに送信されません。 転送の長さが、転送の最大長を超える場合、WinUSB は要求を、転送の最大長より小さい要求に分割して、それを順に送信します。 転送の長さがエンドポイントの **MaxPacketSize** の倍数ではない場合、WinUSB は、転送のサイズを、MaxPacketSize の次の倍数に増加します。 デバイスが要求された量以上のデータを返すと、WinUSB は余分なデータを保存します。 データが前回の読み取り要求時のままである場合、WinUSB は、必要に応じて、それを次の読み取り要求の先頭にコピーし、要求を終了します。
次のコード例は、デバイスのバルクイン エンドポイントからデータを読み取ります。

```ManagedCPlusPlus
BOOL ReadFromBulkEndpoint(WINUSB_INTERFACE_HANDLE hDeviceHandle, UCHAR* pID, ULONG cbSize)
{
    if (hDeviceHandle==INVALID_HANDLE_VALUE)
    {
        return FALSE;
    }

    BOOL bResult = TRUE;

    UCHAR* szBuffer = (UCHAR*)LocalAlloc(LPTR, sizeof(UCHAR)*cbSize);
    
    ULONG cbRead = 0;

    bResult = WinUsb_ReadPipe(hDeviceHandle, *pID, szBuffer, cbSize, &cbRead, 0);
    if(!bResult)
    {
        goto done;
    }

    printf("Read from pipe %d: %s \nActual data read: %d.\n", *pID, szBuffer, cbRead);


done:
    LocalFree(szBuffer);
    return bResult;

}
```

## <a name="step-5-release-the-device-handles"></a>手順 5:デバイス ハンドルを解放する


デバイスへの必要な呼び出しがすべて完了したら、デバイスのファイル ハンドルと WinUSB インターフェイス ハンドルを解放します。 このためには、次の関数を呼び出します。

-   **CloseHandle**: 手順 1 の説明に従って **CreateFile** で作成されたハンドルを解放します。
-   [**WinUsb\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free): デバイスの WinUSB インターフェイス ハンドルを解放します。これは、[**WinUsb\_Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize) によって返されます。

## <a name="step-6-implement-main"></a>手順 6:main を実装する


次のコード例は、コンソール アプリケーションの main 関数を示します。

```ManagedCPlusPlus
int _tmain(int argc, _TCHAR* argv[])
{

    GUID guidDeviceInterface = OSR_DEVICE_INTERFACE; //in the INF file

    BOOL bResult = TRUE;

    PIPE_ID PipeID;

    HANDLE hDeviceHandle = INVALID_HANDLE_VALUE;
    WINUSB_INTERFACE_HANDLE hWinUSBHandle = INVALID_HANDLE_VALUE;
    
    UCHAR DeviceSpeed;
    ULONG cbSize = 0;

    bResult = GetDeviceHandle(guidDeviceInterface, &hDeviceHandle);
    if(!bResult)
    {
        goto done;
    }

    bResult = GetWinUSBHandle(hDeviceHandle, &hWinUSBHandle);
    if(!bResult)
    {
        goto done;
    }

    bResult = GetUSBDeviceSpeed(hWinUSBHandle, &DeviceSpeed);
    if(!bResult)
    {
        goto done;
    }

    bResult = QueryDeviceEndpoints(hWinUSBHandle, &PipeID);
    if(!bResult)
    {
        goto done;
    }

    bResult = SendDatatoDefaultEndpoint(hWinUSBHandle);
    if(!bResult)
    {
        goto done;
    }

    bResult = WriteToBulkEndpoint(hWinUSBHandle, &PipeID.PipeOutId, &cbSize);
    if(!bResult)
    {
        goto done;
    }

    bResult = ReadFromBulkEndpoint(hWinUSBHandle, &PipeID.PipeInId, cbSize);
    if(!bResult)
    {
        goto done;
    }


    system("PAUSE");

done:
    CloseHandle(hDeviceHandle);
    WinUsb_Free(hWinUSBHandle);

    return 0;
}
```

## <a name="next-steps"></a>次の手順


デバイスで等時性エンドポイントがサポートされる場合、[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb) を使用して転送を送信できます。 この機能は、Windows 8.1 でのみサポートされます。

詳細については、「[WinUSB デスクトップ アプリから USB 等時性転送を送信する](getting-set-up-to-use-windows-devices-usb.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[WinUSB](winusb.md)  
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[WinUSB (Winusb.sys) のインストール](winusb-installation.md)  
[パイプ ポリシー修正のための WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)  



