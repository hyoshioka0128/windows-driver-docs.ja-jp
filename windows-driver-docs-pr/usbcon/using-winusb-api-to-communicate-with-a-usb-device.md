---
Description: このトピックでには、WinUSB 関数を使用して、その関数のドライバーとして Winusb.sys を使用している USB デバイスと通信する方法の詳細なチュートリアルが含まれています。
title: WinUSB 関数を使用して USB デバイスにアクセスする方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbe352e1f6be54c250990912a7b0f42e98219772
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356561"
---
# <a name="how-to-access-a-usb-device-by-using-winusb-functions"></a>WinUSB 関数を使用して USB デバイスにアクセスする方法


**要約**

-   デバイスを開き、WinUSB の取得を処理します。
-   デバイス、構成、および、およびすべてのインターフェイスとそのエンドポイントのインターフェイスの設定に関する情報を取得します。
-   一括と割り込みエンドポイント データを読み書きします。

**重要な API**

-   [SetupAPI 関数](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)
-   [WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)

このトピックには、使用する方法の詳細なチュートリアルが含まれています。 [WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)が Winusb.sys 関数ドライバーとして使用している USB デバイスと通信します。

Microsoft Visual Studio 2013 を使用している場合は、WinUSB テンプレートを使用して、スケルトン アプリを作成します。 その場合は、手順 1. ~ 3. をスキップし、このトピックの「手順 4 から続行します。 テンプレートは、デバイスへのファイル ハンドルを開き、後続の操作に必要な WinUSB ハンドルを取得します。 アプリで定義されたデバイスにそのハンドルが格納されている\_device.h 内のデータ構造。

テンプレートの詳細については、書き込み、WinUSB テンプレートに基づく Windows デスクトップ アプリを参照してください。

**注**  WinUSB 関数に必要な Windows XP またはそれ以降。 USB デバイスとの通信に、C/C++ アプリケーションでこれらの関数を使用できます。 Microsoft では、WinUSB のマネージ API は提供されません。

## <a href="" id="pre"></a>前提条件


このチュートリアルに、次のものが適用されます。

-   この情報は、Windows 8.1、Windows 8、Windows 7、Windows Server 2008、Windows Vista のバージョンの Windows に適用されます。
-   デバイスの機能のドライバーとして Winusb.sys をインストールしておきます。 このプロセスの詳細については、次を参照してください。 [WinUSB (Winusb.sys) インストール](winusb-installation.md)します。
-   このトピックの例がに基づいて、 [OSR USB FX2 Learning Kit デバイス](http://www.osronline.com/)します。 これらの例を使用すると、他の USB デバイスにプロシージャを拡張するのにことができます。

## <a href="" id="setup"></a>手順 1:WinUSB テンプレートに基づくスケルトン アプリを作成します。


USB デバイスにアクセスするには、Windows Driver Kit (WDK) (デバッグ ツールの Windows) との統合環境に含まれる WinUSB テンプレートに基づくスケルトン アプリを作成して開始し、Microsoft Visual Studio.You は開始点としてテンプレートを使用することができます。

については、テンプレート コードを作成、ビルド、展開、およびスケルトン アプリをデバッグする方法は、「 [WinUSB テンプレートに基づく Windows デスクトップ アプリを記述](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)します。

テンプレートを使用してデバイスを列挙する[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)ルーチンが開き、ファイルは、デバイスの処理し、後続のタスクに必要な WinUSB インターフェイスのハンドルを作成します。 デバイス ハンドルを取得し、デバイスをオープンするコード例を参照してください。[テンプレート コードの説明](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)します。

## <a href="" id="query"></a>手順 2:記述子の USB デバイスを照会します。


次に、デバイスの速度、インターフェイスの記述子、関連するエンドポイント、およびそのパイプなどの USB に固有の情報については、デバイスのクエリを実行します。 プロシージャは、USB デバイス ドライバーを使用する 1 つに似ています。 ただし、アプリケーションが呼び出すことでデバイスのクエリを完了[ **WinUsb\_いる出力**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)します。

USB に固有の情報の取得を呼び出すこと WinUSB 関数を次に示します。

-   その他のデバイスの情報です。

    呼び出す[ **WinUsb\_QueryDeviceInformation** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querydeviceinformation)デバイスのデバイス記述子から情報を要求します。 デバイスの速度を取得するには、デバイスを設定\_(0x01) の速度が、 *InformationType*パラメーター。 関数は、速度低下 (0x01) または高速接続 (0x03) を返します。

-   記述子をインターフェイスします。

    呼び出す[ **WinUsb\_QueryInterfaceSettings** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)デバイスのインターフェイスを対応するインターフェイスの記述子を取得する処理を渡します。 WinUSB インターフェイスのハンドルは、最初のインターフェイスに対応します。 OSR Fx2 デバイスなど、一部の USB デバイスは、任意の代替設定がない場合の 1 つだけインターフェイスをサポートします。 そのため、これらのデバイスに対して、 *AlternateSettingNumber*パラメーターが 0 に設定されているし、関数には、1 回だけが呼び出されます。 **WinUsb\_QueryInterfaceSettings**呼び出し元が割り当てた塗りつぶします[ **USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor) (、で渡された構造体*UsbAltInterfaceDescriptor*パラメーター) インターフェイスに関する情報を使用します。 インターフェイス内のエンドポイントの数を設定するなど、 **bNumEndpoints**のメンバー **USB\_インターフェイス\_記述子**します。

    複数のインターフェイスをサポートするデバイスの場合は、呼び出す[ **WinUsb\_GetAssociatedInterface** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface)の代替設定を指定することで関連付けられているインターフェイスのインターフェイスのハンドルを取得するには*AssociatedInterfaceIndex*パラメーター。

-   エンドポイント

    呼び出す[ **WinUsb\_QueryPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe)各インターフェイス上の各エンドポイントに関する情報を取得します。 **WinUsb\_QueryPipe**設定呼び出し元が割り当てた[ **WINUSB\_パイプ\_情報**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)に関する情報を含む構造体、指定したエンドポイントのパイプです。 エンドポイントのパイプは、0 から始まるインデックスによって識別されの値より小さい必要があります、 **bNumEndpoints**を前の呼び出しで取得されるインターフェイスの記述子のメンバー [ **WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)します。 OSR Fx2 デバイスには、3 つのエンドポイントが 1 つのインターフェイスがあります。 このデバイスの場合、関数の*AlternateInterfaceNumber*パラメーターが 0、およびの値に設定されている、 *PipeIndex*パラメーターが 0 から 2 には異なります。

    パイプの種類を判断するに調べて、 [ **WINUSB\_パイプ\_情報**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)構造体の**PipeInfo**メンバー。 このメンバーのいずれかに設定されます、 [ **USBD\_パイプ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ne-usb-_usbd_pipe_type)列挙値。UsbdPipeTypeControl、UsbdPipeTypeIsochronous、UsbdPipeTypeBulk、または UsbdPipeTypeInterrupt します。 OSR USB FX2 デバイス サポート、割り込みパイプ、一括でパイプ、および一括アウト パイプでは、そのため**PipeInfo** UsbdPipeTypeInterrupt または UsbdPipeTypeBulk のいずれかに設定されます。 UsbdPipeTypeBulk 値は、一括のパイプを識別しますが、パイプの方向を行いません。 方向に関する情報に格納されているパイプ アドレスのビットでエンコードされた、 **WINUSB\_パイプ\_情報**構造体の**PipeId**メンバー。 パイプの方向を決定する最も簡単な方法は、渡す、 **PipeId** Usb100.h からの値を次のマクロのいずれか。

    -   `USB_ENDPOINT_DIRECTION_IN (PipeId)`マクロ返します**TRUE**方向がである場合。
    -   `USB_ENDPOINT_DIRECTION_OUT(PipeId)`マクロを返します**TRUE**方向が out 場合。

    アプリケーションを使用して、 **PipeId**など WinUSB 関数への呼び出しでのデータ転送に使用するパイプを識別する値[ **WinUsb\_ReadPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe) (このトピックの「I/O 要求の問題」セクションでは、説明例では、3 つすべてを格納するように**PipeId**後で使用する値。

次のコード例では、WinUSB インターフェイスのハンドルで指定されているデバイスの速度を取得します。

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

次のコード例では、WinUSB インターフェイスのハンドルで指定されている USB デバイスのさまざまな記述子を照会します。 関数の例では、サポートされているエンドポイントと、パイプの識別子の型を取得します。 例では、後で使用できる 3 つすべての PipeId 値を格納します。

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

## <a href="" id="control"></a>手順 3:コントロールの転送を既定のエンドポイントに送信します。


次に、既定のエンドポイントへのコントロール要求を発行するデバイスと通信します。

すべての USB デバイスでは、既定のエンドポイントだけでなくインターフェイスに関連付けられているエンドポイントがあります。 既定のエンドポイントの主な目的では、デバイスを構成するために使用できる情報をホストを提供します。 ただし、デバイスはデバイスに固有の目的で、既定のエンドポイントを使用することができますも。 たとえば、OSR USB FX2 デバイスは、ライトのバーとデジタル ディスプレイの 7 つのセグメントを制御するのに既定のエンドポイントを使用します。

管理コマンドは、特定の要求と、省略可能なデータ バッファーを指定する要求コードを含む、8 バイト セットアップ パケットので構成されます。 要求のコードとバッファーの形式はベンダー定義です。 この例では、アプリケーションは、ライトのバーを制御するデバイスにデータを送信します。 ライトのバーを設定するコードは、便宜上セットとして定義されている 0xD8\_BARGRAPH\_表示します。 この要求では、適切なビットを設定する要素を点灯する必要がありますを指定する 1 バイトのデータ バッファーをデバイスが必要です。

アプリケーション設定できますこのユーザー インターフェイス (UI) からなど、ライトのバーの要素を点灯するを指定する 8 つのチェック ボックス コントロールのセットを提供することで。 指定された要素は、バッファー内の適切なビットに対応します。 UI コードを避けるためには、このセクションのコード例は、代替のライトが点灯を取得するために、ビットを設定します。

**コントロールの要求を発行するのにには、次の手順を使用します。**

1.  1 バイトのデータ バッファーを割り当てるし、適切なビットを設定する必要がありますが点灯している要素を指定しているバッファーにデータを読み込みます。
2.  呼び出し元が割り当てたでセットアップ パケットを構築[ **WINUSB\_セットアップ\_パケット**](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)構造体。 次のように、要求の種類とデータを表すメンバーを初期化します。
    -   **RequestType**メンバーは、要求の方向を指定します。 ホストからデバイスへのデータ転送を示す 0 に設定されます。 デバイスからホストへの転送では、修飾子の一覧を 1 に設定します。
    -   **要求**メンバー 0xD8 は、この要求のベンダー定義のコードに設定されます。 便宜上、セットとして定義されている\_BARGRAPH\_表示します。
    -   **長さ**メンバー データ バッファーのサイズに設定されます。
    -   **インデックス**と**値**メンバーは 0 に設定されているため、この要求に必要ないです。

3.  呼び出す[ **WinUsb\_ControlTransfer** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer) WinUSB インターフェイス ハンドルのデバイスのセットアップ パケットの場合、データ バッファーを渡すことで、既定のエンドポイントに要求を送信します。 関数は、受信デバイスに転送されたバイト数、 *LengthTransferred*パラメーター。

次のコード例では、ライトのバーにあるライトを制御する指定された USB デバイスを制御要求を送信します。

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

## <a href="" id="io"></a>手順 4:I/O 要求を発行します。


次に、データを送信すると、読み取りのために使用して、それぞれの書き込み要求、デバイスの一括でおよび一括アウト エンドポイントにします。 OSR USB FX2 デバイスでは、これら 2 つのエンドポイントは、デバイスは、データを一括でエンドポイントから一括アウト エンドポイントに移動するために、ループバックに対して構成されます。 データの値を変更したり、新しいデータを追加しません。 ループバック構成では、読み取り要求は、最新の書き込み要求によって送信されたデータを読み取ります。 WinUSB は書き込みを送信するために、次の機能を提供し、要求を読み取ります。

-   [**WinUsb\_WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)
-   [**WinUsb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)

**書き込み要求を送信するには**

1.  バッファーを割り当てるし、それをデバイスへの書き込みにする、データを入力します。 アプリケーションが RAW を設定していない場合、バッファーのサイズに制限はありません\_パイプのポリシーの種類として IO。 WinUSB は、必要な場合に、バッファーを適切なサイズのチャンクに分割します。 生場合\_IO の設定、バッファーのサイズが WinUSB でサポートされる最大転送サイズによって制限されます。
2.  呼び出す[ **WinUsb\_WritePipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)デバイスにバッファーを書き込めません。 デバイスの場合、一括アウト パイプのパイプ識別子 WinUSB インターフェイスのハンドルを渡す (」の説明に従って、[記述子の USB デバイスを照会](#query)このトピックの「)、およびバッファー。 デバイスに実際に書き込まれるバイト数を返します、 *bytesWritten*パラメーター。 *Overlapped*にパラメーターが設定されている**NULL**同期操作を要求します。 非同期書き込み要求を実行するには、次のように設定します。 *Overlapped*へのポインター、 **OVERLAPPED**構造体。

USB スタックを長さ 0 のデータが含まれている要求が転送されるを記述します。 転送の長さが最大転送サイズより大きい値の場合は、WinUSB は長さが最大転送の小さな要求に要求を分割し、連続的に送信します。
次のコード例では、文字列が割り当てし、デバイスの一括アウト エンドポイントに送信します。

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

**読み取り要求を送信するには**

-   呼び出す[ **WinUsb\_ReadPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)デバイスの一括でエンドポイントからデータを読み取る。 デバイスの一括でのエンドポイントと適切なサイズの空きバッファーのパイプ識別子 WinUSB インターフェイスのハンドルを渡します。 関数が戻るとき、バッファーには、デバイスから読み取られたデータが含まれています。 関数ので読み取られたバイト数が返される*bytesRead*パラメーター。 読み取り要求は、バッファーはパケットの最大サイズの倍数である必要があります。

長さ 0 の読み取り要求が成功して直ちに完了し、下位のスタックは送信されません。 転送の長さが最大転送サイズより大きい値の場合は、WinUSB は長さが最大転送の小さな要求に要求を分割し、連続的に送信します。 転送の長さが、エンドポイントの倍数ではないかどうか**この**、WinUSB この倍数に転送のサイズが増加します。 デバイスは、要求された以上のデータを返します、WinUSB は余分なデータを保存します。 データは、前の読み取り要求からは、WinUSB は次の読み取り要求の先頭にコピーし、必要に応じて、要求を完了します。
次のコード例では、デバイスの一括でエンドポイントからデータを読み取ります。

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

## <a name="step-5-release-the-device-handles"></a>手順 5:デバイス ハンドルを解放します。


デバイスに必要なすべての呼び出しを完了すると後、は、ファイル ハンドルとデバイスの WinUSB インターフェイスのハンドルをリリースします。 これは、次の関数を呼び出します。

-   **CloseHandle**によって作成されたハンドルを解放する**CreateFile**手順 1. で説明するようにします。
-   [**WinUsb\_Free** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)によって返されると、デバイスの WinUSB インターフェイスのハンドルを解放する[ **WinUsb\_初期化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)します。

## <a name="step-6-implement-main"></a>手順 6:Main の実装


次のコード例では、コンソール アプリケーションの main 関数を示します。

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

## <a name="next-steps"></a>次のステップ


デバイスは、アイソクロナス エンドポイントをサポートする場合は使用できます[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)転送を送信します。 この機能は、Windows 8.1 でのみサポートされます。

詳細については、次を参照してください。 [WinUSB デスクトップ アプリから送信 USB アイソクロナス転送](getting-set-up-to-use-windows-devices-usb.md)します。

## <a name="related-topics"></a>関連トピック
[WinUSB](winusb.md)  
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[WinUSB (Winusb.sys) のインストール](winusb-installation.md)  
[ポリシーの変更をパイプ WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB テンプレートに基づく Windows デスクトップ アプリを作成します。](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)  



