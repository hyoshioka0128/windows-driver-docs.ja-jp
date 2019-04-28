---
title: COPP で使用される暗号プリミティブ
description: COPP で使用される暗号プリミティブ
ms.assetid: a14f6f4c-75fd-41a3-93f8-86c9908a2343
keywords:
- WDK COPP、暗号化の保護をコピーします。
- ビデオのコピー防止 WDK COPP、暗号化
- COPP WDK DirectX va なので、暗号化
- ビデオの WDK COPP、暗号化の保護
- WDK COPP の暗号化
- WDK COPP の暗号化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81c95ae5a9ecde73889c686ab64c7880957c931f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371488"
---
# <a name="cryptographic-primitives-used-by-copp"></a>COPP で使用される暗号プリミティブ


## <span id="ddk_cryptographic_primitives_used_by_copp_gg"></span><span id="DDK_CRYPTOGRAPHIC_PRIMITIVES_USED_BY_COPP_GG"></span>


このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

COPP では、次の暗号化プリミティブを使用します。

<span id="Public_key_cryptography"></span><span id="public_key_cryptography"></span><span id="PUBLIC_KEY_CRYPTOGRAPHY"></span>公開キーの暗号化  
COPP では、公開キーの暗号化と復号化キーを 2,048 ビット RSA アルゴリズムが必要です。 RSA アルゴリズムの詳細については、次を参照してください。、 [RSA Laboratories](https://go.microsoft.com/fwlink/p/?linkid=70411) web サイト。

<span id="Digital_certificates"></span><span id="digital_certificates"></span><span id="DIGITAL_CERTIFICATES"></span>デジタル証明書  
COPP eXtensible rights Markup Language (XrML) デジタル証明書を使用します。

<span id="Message_authentication_code__MAC_"></span><span id="message_authentication_code__mac_"></span><span id="MESSAGE_AUTHENTICATION_CODE__MAC_"></span>メッセージ認証コード (MAC)  
COPP を 1 つのキー暗号化ブロック チェーン (CBC) を使用して-メッセージの信頼性の MAC (OMAC) のモード。 OMAC は、Advanced Encryption Standard (AES) に基づいています。 AES の詳細については、次を参照してください。、 [RSA Laboratories](https://go.microsoft.com/fwlink/p/?linkid=70411) web サイト。 OMAC の詳細については、次を参照してください。、 [OMAC 1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)します。

 

 





