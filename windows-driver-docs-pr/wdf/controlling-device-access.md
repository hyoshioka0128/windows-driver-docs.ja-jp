---
title: デバイス アクセスの制御
description: デバイス アクセスの制御
ms.assetid: E4FF73B3-87D0-458E-A042-E5A8F3DB1677
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6a8c24d0b41308fe5fec4f530ec04ac382ce89b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579275"
---
# <a name="controlling-device-access"></a>デバイス アクセスの制御


UMDF ドライバーのホスト プロセスは、ローカル サービス アカウントのコンテキストで実行されます。 ドライバーは、その他のデバイスにアクセスする必要があります。 または許可されていないコンポーネントがローカル サービス アカウントへのアクセスを一般化します。

Windows 8 以降、オペレーティング システムには、UMDF ドライバーを識別するセキュリティ識別子 (SID) が含まれています。 この SID をデバイスのセキュリティ要件に含めても、デバイスやコンポーネントは、ローカル サービス アカウントから他の要求からのアクセスを防ぎながら UMDF ドライバーへのアクセスを許可できます。

UMDF ドライバーの SID が SDDL\_ユーザー\_モード\_sddl.h されて、ドライバー、および定義します。 この SID の完全な形式は次のとおりです。

```cpp
S-1-5-84-0-0-0-0-0
```

この SID の省略形では、UD です。 このコードは以降 Windows 8 で使用できます。

外部には、UMDF ドライバーをドライバーにデバイス オブジェクトを作成する前に、INF ファイルで、または driver では、SID を指定できます。

## <a name="specifying-device-security-in-an-inf-file"></a>INF ファイルでデバイスのセキュリティを指定します。


INF ファイルで、省略形または SID の完全指定の形式のいずれかを使用することができます。

省略形は、Windows 8 以降を入手できます。

```cpp
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;UD)"   
```

Windows 8 より前のオペレーティング システムには、完全に指定した形式を使用する必要があります。

```cpp
HKR,,Security,,"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;S-1-5-84-0-0-0-0-0)"       
```

## <a name="specifying-device-security-in-a-kmdf-driver"></a>KMDF ドライバーでは、デバイスのセキュリティを指定します。


ドライバーのセキュリティ要件を指定するには、のみが Windows 8 以降を使用できる省略形を使用する必要があります。 たとえば、KMDF ドライバーでしたからアクセスできるようにそのデバイスに UMDF ドライバー、以下を使用しています。

```cpp
RtlInitUnicodeString(&sddlString, L"D:P(A;;GA;;;BA)(A;;GA;;;SY)(A;;GA;;;UD)");
status = WdfDeviceInitAssignSDDLString(DeviceInit, &sddlString);
```

 

 





