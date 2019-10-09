---
Description: このトピックでは、winusb 機能を使用して、Winusb を関数ドライバーとして使用している USB デバイスと通信する方法について詳しく説明します。
title: WinUSB 関数を使用して USB デバイスにアクセスする方法
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: d3ab1328cab41bfcd7281d8ea8356041edfc4820
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007585"
---
# <a name="how-to-access-a-usb-device-by-using-winusb-functions"></a>WinUSB 関数を使用して USB デバイスにアクセスする方法


**概要**

-   デバイスを開いて WinUSB ハンドルを取得しています。
-   すべてのインターフェイス、、およびそれらのエンドポイントのデバイス、構成、およびインターフェイスの設定に関する情報を取得します。
-   データの読み取りと書き込みを行って、エンドポイントを一括して中断します。

**重要な API**

-   [Setupapi.log 関数](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)
-   [WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)

このトピックでは、winusb[機能](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を使用して、winusb を関数ドライバーとして使用している usb デバイスと通信する方法について詳しく説明します。

Microsoft Visual Studio 2013 を使用している場合は、WinUSB テンプレートを使用してスケルトンアプリを作成します。 その場合は、手順 1. ~ 3. をスキップし、このトピックの手順 4. を続行します。 このテンプレートは、デバイスへのファイルハンドルを開き、後続の操作に必要な WinUSB ハンドルを取得します。 そのハンドルは、アプリケーション定義のデバイスの @ no__t-0DATA 構造に格納されています。

テンプレートの詳細については、「WinUSB テンプレートに基づいて Windows デスクトップアプリを作成する」を参照してください。

**注**  WinUSB functions には Windows XP 以降が必要です。 C/C++アプリケーションでこれらの関数を使用して、USB デバイスと通信することができます。 Microsoft は WinUSB 用のマネージ API を提供していません。

## <a href="" id="pre"></a>応募


このチュートリアルには、次の項目が適用されます。

-   この情報は、Windows 8.1、Windows 8、Windows 7、Windows Server 2008、Windows Vista の各バージョンの windows に適用されます。
-   デバイスの関数ドライバーとして Winusb .sys がインストールされていること。 このプロセスの詳細については、 [winusb (winusb .sys) のインストール](winusb-installation.md)に関する説明を参照してください。
-   このトピックの例は、 [OSR USB FX2 Learning Kit デバイス](http://www.osronline.com/)に基づいています。 これらの例を使用して、他の USB デバイスにプロシージャを拡張できます。

## <a href="" id="setup"></a>手順 1:WinUSB テンプレートに基づいてスケルトンアプリを作成する


USB デバイスにアクセスするには、まず、Windows Driver Kit (WDK) の統合環境に含まれる WinUSB テンプレートに基づくスケルトンアプリを作成し (Windows 用のデバッグツールを使用)、Microsoft Visual Studio ます。このテンプレートは出発点として使用できます。

テンプレートコード、スケルトンアプリを作成、ビルド、展開、デバッグする方法の詳細については、「 [WinUSB テンプレートに基づいて Windows デスクトップアプリ](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)を作成する」を参照してください。

このテンプレートは、 [setupapi.log](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)ルーチンを使用してデバイスを列挙し、デバイスのファイルハンドルを開き、後続のタスクに必要な winusb インターフェイスハンドルを作成します。 デバイスハンドルを取得してデバイスを開くコードの例については、「[テンプレートコードの説明](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)」を参照してください。

## <a href="" id="query"></a>手順 2:デバイスで USB 記述子を照会する


次に、デバイスの速度、インターフェイス記述子、関連するエンドポイント、パイプなど、USB 固有の情報をデバイスに照会します。 この手順は、USB デバイスドライバーが使用する手順と似ています。 ただし、アプリケーションは[**Winusb @ no__t-2GetDescriptor**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)を呼び出すことによって、デバイスのクエリを完了します。

次の一覧は、USB 固有の情報を取得するために呼び出すことができる WinUSB 関数を示しています。

-   追加のデバイス情報。

    [**Winusb @ no__t-2QueryDeviceInformation**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querydeviceinformation)を呼び出して、デバイスのデバイス記述子の情報を要求します。 デバイスの速度を取得するには、 *Informationtype*パラメーターにデバイス @ NO__T-0speed (0x01) を設定します。 関数は、LowSpeed (0x01) または HighSpeed (0x03) を返します。

-   インターフェイス記述子

    [**Winusb @ no__t-2QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)を呼び出し、デバイスのインターフェイスハンドルを渡して、対応するインターフェイス記述子を取得します。 WinUSB インターフェイスハンドルは、最初のインターフェイスに対応します。 OSR Fx2 デバイスなど、一部の USB デバイスでは、代替設定のないインターフェイスが1つだけサポートされます。 そのため、これらのデバイスの場合、 *Alternatesettingnumber*パラメーターは0に設定され、関数は1回だけ呼び出されます。 **Winusb @ no__t-1QueryInterfaceSettings**は、呼び出し元が割り当てた[**USB @ NO__T-4interface @ NO__T-5descriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)構造体 ( *us・ tinterfacedescriptor*パラメーターで渡されます) に、インターフェイスに関する情報を入力します。 たとえば、インターフェイス内のエンドポイントの数は、 **USB @ no__t-2INTERFACE @ no__t-3DESCRIPTOR**の**bnumendpoints**メンバーで設定されます。

    複数のインターフェイスをサポートするデバイスの場合は、 [**winusb @ no__t-2GetAssociatedInterface**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface)を呼び出して、関連するインターフェイスのインターフェイスハンドルを取得します。そのためには、 *AssociatedInterfaceIndex*パラメーターで別の設定を指定します。

-   エンドポイント

    各インターフェイスの各エンドポイントに関する情報を取得するには[ **、Winusb @ no__t-2QueryPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe)を呼び出します。 **Winusb @ no__t-1QueryPipe**は、呼び出し元が割り当てた[**winusb @ NO__T-4pipe @ NO__T-5information**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)構造体に、指定されたエンドポイントのパイプに関する情報を設定します。 エンドポイントのパイプは、0から始まるインデックスによって識別されます。これは、前の[**Winusb @ no__t-3QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)の呼び出しで取得されるインターフェイス記述子の**bnumendpoints**メンバーの値未満である必要があります。 OSR Fx2 デバイスには、3つのエンドポイントを持つインターフェイスが1つあります。 このデバイスの場合、関数の*AlternateInterfaceNumber*パラメーターは0に設定され、 *PipeIndex*パラメーターの値は0から2に変わります。

    パイプの種類を確認するには、 [**Winusb @ no__t-2PIPE @ no__t-3INFORMATION**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)構造体の**PipeInfo**メンバーを調べます。 このメンバーは、 [**USBD @ no__t-2PIPE @ no__t-3TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ne-usb-_usbd_pipe_type)列挙値のいずれかに設定されます。UsbdPipeTypeControl、UsbdPipeTypeIsochronous、UsbdPipeTypeBulk、または UsbdPipeTypeInterrupt。 OSR USB FX2 デバイスでは、割り込みパイプ、一括インパイプ、および一括出力パイプがサポートされているため、 **PipeInfo**は UsbdPipeTypeInterrupt または UsbdPipeTypeBulk のいずれかに設定されます。 UsbdPipeTypeBulk 値は、バルクパイプを識別しますが、パイプの方向を指定しません。 方向情報は、パイプアドレスの上位ビットでエンコードされます。これは、 **Winusb @ no__t-1PIPE @ no__t-2information** Structure の**PipeId**メンバーに格納されています。 パイプの方向を決定する最も簡単な方法は、Usb100 から次のマクロのいずれかに**PipeId**値を渡すことです。

    -   @No__t-0 マクロは、方向がにある場合に**TRUE**を返します。
    -   @No__t-0 マクロは、方向が out の場合に**TRUE**を返します。

    このアプリケーションでは、 **PipeId**値を使用して winusb 関数の呼び出しでデータ転送に使用するパイプを識別し[**ます (こ**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)のトピックの「Issue i/o Requests」セクションで説明します)。この例では、次の3つ**をすべて格納します。PipeId**値は後で使用するために使用します。

次のコード例では、WinUSB インターフェイスハンドルによって指定されたデバイスの速度を取得します。

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

次のコード例では、WinUSB インターフェイスハンドルによって指定された USB デバイスのさまざまな記述子に対してクエリを行います。 この例の関数は、サポートされているエンドポイントとそのパイプ識別子の型を取得します。 この例では、3つの PipeId 値すべてを後で使用できるように格納します。

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

## <a href="" id="control"></a>手順 3:既定のエンドポイントに制御転送を送信する


次に、既定のエンドポイントに制御要求を発行して、デバイスと通信します。

すべての USB デバイスには、インターフェイスに関連付けられているエンドポイントに加えて、既定のエンドポイントがあります。 既定のエンドポイントの主な目的は、ホストにデバイスの構成に使用できる情報を提供することです。 ただし、デバイスでは、デバイス固有の目的で既定のエンドポイントを使用することもできます。 たとえば、OSR USB FX2 デバイスは、既定のエンドポイントを使用して、ライトバーと7セグメントのデジタルディスプレイを制御します。

制御コマンドは、8バイトのセットアップパケットで構成されます。このパケットには、特定の要求を指定する要求コードと、オプションのデータバッファーが含まれています。 要求コードとバッファー形式は、vendor で定義されています。 この例では、アプリケーションがデバイスにデータを送信してライトバーを制御します。 ライトバーを設定するコードは0xD8 です。これは、SET @ no__t-0BARGRAPH @ no__t-1DISPLAY として便利なように定義されています。 この要求の場合、デバイスには、適切なビットを設定することによって、どの要素を点灯させるかを指定する1バイトのデータバッファーが必要です。

アプリケーションでは、ユーザーインターフェイス (UI) を使用してこれを設定できます。たとえば、一連のチェックボックスコントロールを使用して、ライトバーのどの要素を点灯させるかを指定します。 指定された要素は、バッファー内の適切なビットに対応します。 UI コードを避けるために、このセクションのコード例では、代替ライトが点灯するようにビットを設定しています。

**コントロール要求を発行するには、次の手順に従います。**

1.  1バイトのデータバッファーを割り当てて、適切なビットを設定して、lit にする必要がある要素を指定するバッファーにデータを読み込みます。
2.  呼び出し元が割り当てた[**Winusb @ no__t-2SETUP @ no__t-3packet**](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)構造体にセットアップパケットを構築します。 次のように、メンバーを初期化して、要求の種類とデータを表します。
    -   **RequestType**メンバーは、要求の方向を指定します。 これは、ホストからデバイスへのデータ転送を示す0に設定されます。 デバイスからホストへの転送では、RequestType を1に設定します。
    -   **要求**メンバーは、この要求のベンダー定義コード0xD8 に設定されます。 これは、SET @ no__t-0BARGRAPH @ no__t-1DISPLAY として便利なように定義されています。
    -   **Length**メンバーは、データバッファーのサイズに設定されます。
    -   **インデックス**と**値**のメンバーは、この要求には必要ありません。したがって、0に設定されます。

3.  [**Winusb @ no__t-2ControlTransfer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)を呼び出して、デバイスの winusb インターフェイスハンドル、セットアップパケット、およびデータバッファーを渡して、既定のエンドポイントに要求を送信します。 関数は、転送された*長さ*のパラメーターでデバイスに転送されたバイト数を受け取ります。

次のコード例では、指定された USB デバイスにコントロール要求を送信して、ライトバーのライトを制御します。

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

## <a href="" id="io"></a>手順 4:I/o 要求を発行する


次に、読み取り要求と書き込み要求に使用できるデバイスの一括受信エンドポイントと一括送信エンドポイントにデータを送信します。 OSR USB FX2 デバイスでは、これら2つのエンドポイントはループバック用に構成されているため、デバイスはデータを一括送信エンドポイントから一括送信エンドポイントに移動します。 データの値を変更したり、新しいデータを追加したりすることはありません。 ループバック構成の場合、読み取り要求は、最新の書き込み要求によって送信されたデータを読み取ります。 WinUSB には、書き込み要求と読み取り要求を送信するための次の機能が用意されています。

-   [**WinUsb @ no__t-2WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)
-   [**WinUsb @ no__t-2ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)

**書き込み要求を送信するには**

1.  バッファーを割り当てて、デバイスに書き込むデータを入力します。 アプリケーションで RAW @ no__t-0IO がパイプのポリシーの種類として設定されていない場合、バッファーサイズに制限はありません。 WinUSB は、必要に応じて、バッファーを適切にサイズ設定されたチャンクに分割します。 RAW @ no__t-0IO が設定されている場合、バッファーのサイズは WinUSB でサポートされている最大転送サイズによって制限されます。
2.  デバイスにバッファーを書き込むには、 [**Winusb @ no__t-2WritePipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)を呼び出します。 デバイスの WinUSB インターフェイスハンドル、bulk out パイプのパイプ識別子 (このトピックの「デバイスでの[USB 記述子のクエリ](#query)」を参照)、およびバッファーを渡します。 関数は、バイト数を返します。このバイト数は、*書き込み*パラメーターでデバイスに実際に書き込まれます。 *重複*するパラメーターを**NULL**に設定すると、同期操作が要求されます。 非同期書き込み要求を実行するには **、オーバーラップされた構造体**へのポインターに*overlapped*を設定します。

長さ0のデータを含む書き込み要求は、USB スタックを介して転送されます。 転送の長さが最大転送長を超える場合、WinUSB は要求を最大転送長の小さな要求に分割し、直列に送信します。
次のコード例では、文字列を割り当てて、デバイスの一括送信エンドポイントに送信します。

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

-   デバイスの一括エンドポイントからデータを読み取るには、 [**Winusb @ no__t-2ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)を呼び出します。 デバイスの WinUSB インターフェイスハンドル、一括入力エンドポイントのパイプ識別子、および適切にサイズ設定された空のバッファーを渡します。 関数から制御が戻ると、バッファーには、デバイスから読み取られたデータが格納されます。 読み取られたバイト数は、関数の*Bytesread*パラメーターで返されます。 読み取り要求の場合、バッファーは最大パケットサイズの倍数である必要があります。

長さ0の読み取り要求は、正常に完了するとすぐに完了し、スタックには送信されません。 転送の長さが最大転送長を超える場合、WinUSB は要求を最大転送長の小さな要求に分割し、直列に送信します。 転送の長さがエンドポイントの**MaxPacketSize**の倍数ではない場合、winusb は、MaxPacketSize の次の倍数に転送のサイズを増やします。 デバイスが要求された数よりも多くのデータを返す場合、WinUSB は余分なデータを保存します。 前の読み取り要求からデータが残っている場合、WinUSB は、次の読み取り要求の先頭にコピーし、必要に応じて要求を完了します。
次のコード例では、デバイスの一括エンドポイントからデータを読み取ります。

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

## <a name="step-5-release-the-device-handles"></a>手順 5:デバイスハンドルを解放する


デバイスに対して必要な呼び出しをすべて完了したら、ファイルハンドルと、デバイスの WinUSB インターフェイスハンドルを解放します。 そのためには、次の関数を呼び出します。

-   **CloseHandle** 。手順 1. で説明したように、 **CreateFile**によって作成されたハンドルを解放します。
-   [**Winusb @ no__t-2Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)は、winusb [ **@ No__t-5initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)によって返されるデバイスの winusb インターフェイスハンドルを解放するために使用します。

## <a name="step-6-implement-main"></a>手順 6:Main を実装する


次のコード例は、コンソールアプリケーションの main 関数を示しています。

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


デバイスでアイソクロナスエンドポイントがサポートされている場合は、 [Winusb 機能](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を使用して転送を送信できます。 この機能は、Windows 8.1 でのみサポートされています。

詳細については、「 [winusb デスクトップアプリから usb アイソクロナス転送を送信する](getting-set-up-to-use-windows-devices-usb.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[WinUSB](winusb.md)  
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[WinUSB (Winusb .sys) のインストール](winusb-installation.md)  
[パイプポリシーを変更するための WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB テンプレートに基づいて Windows デスクトップアプリを作成する](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)  



