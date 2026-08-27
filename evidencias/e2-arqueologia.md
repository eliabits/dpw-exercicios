## PERGUNTAS DO QUESTIONÁRIO

---
# 1 - Quantos commits o repositório tem?
**- comando utilizado:** 
eliab@ELIABS MINGW64 /tmp/nest (master)
$ git rev-list --count HEAD
- resposta ao comando:

21672

---

# 2 - Qual foi o primeiro commit, e em que data
**- comando utilizado:** 
eliab@ELIABS MINGW64 /tmp/nest (master)
$ git log --reverse --format="%h - %ad - %s" --date=format:"%d/%m/%Y %H:%M"

-resposta ao comando:
f7c8d10fb - 08/01/2017 15:09 - Initial commit

---

# 3	Quem mais modificou packages/core/injector/injector.ts?
- comando utilizado:
eliab@ELIABS MINGW64 /tmp/nest (master)
$ git log --format="%an" -- packages/core/injector/injector.ts | sort | uniq -c | sort -nr

- resposta ao comando:

     90 Kamil Myśliwiec


---
# 4	O que mudou no último commit que tocou esse arquivo?
- comando utilizado: 
eliab@ELIABS MINGW64 /tmp/nest (master)
$ git show

- resposta ao comando: 

commit 3f8a0ce1832fb30053f55856088371b097bbf7e1 (HEAD -> master, origin/master, origin/HEAD)
Author: Tushar Pagar <240662211+tushardev-365@users.noreply.github.com>
Date:   Fri Aug 21 11:16:49 2026 +0000

    fix(microservices): handle non-json mqtt response packets gracefully
    
    ClientMqtt.createResponseCallback parsed every incoming reply with an
    unguarded JSON.parse. A non-json payload on a subscribed reply topic threw
    inside the async mqtt message listener, producing an unhandled rejection,
    and the pending request observable never settled.
    
    Every other transport already guards this parse: ClientRedis falls back to
    the raw content with a debug log, and the mqtt, redis and rmq servers all
    parse defensively. This applies the same guard ClientRedis uses, passing
    the raw content to the deserializer.

diff --git a/packages/microservices/client/client-mqtt.ts b/packages/microservices/client/client-mqtt.ts
index bcd4873ae..33e0d5645 100644
--- a/packages/microservices/client/client-mqtt.ts
+++ b/packages/microservices/client/client-mqtt.ts
@@ -201,7 +201,15 @@ export class ClientMqtt extends ClientProxy<MqttEvents, MqttStatus> {
 
   public createResponseCallback(): (channel: string, buffer: Buffer) => any {
     return async (channel: string, buffer: Buffer) => {
-      const packet = JSON.parse(buffer.toString());
+      let packet: any;
+      try {
+        packet = JSON.parse(buffer.toString());
+      } catch (err) {
+        this.logger.debug(
+          'MQTT response packet is not in json format, bypassing...',
+        );
+        packet = buffer.toString();
+      }
       const { err, response, isDisposed, id } =
         await this.deserializer.deserialize(packet);
 
diff --git a/packages/microservices/test/client/client-mqtt.spec.ts b/packages/microservices/test/client/client-mqtt.spec.ts
index 87f461c5b..74f768c5f 100644
--- a/packages/microservices/test/client/client-mqtt.spec.ts
+++ b/packages/microservices/test/client/client-mqtt.spec.ts
@@ -224,6 +224,27 @@ describe('ClientMqtt', () => {
         expect(callback).not.toHaveBeenCalled();
       });
     });
+    describe('message is not in json format', () => {
+      it('should not throw and pass the raw content to the deserializer', async () => {
+        callback = vi.fn();
+        const bufferMessage = Buffer.from(
+          `${responseMessage.id}|${responseMessage.response}`,
+        );
+        vi.spyOn(
+          Reflect.get(client, 'deserializer'),
+          'deserialize',
+        ).mockResolvedValue(responseMessage as any);
+        subscription = client.createResponseCallback();
+
+        client['routingMap'].set(responseMessage.id, callback);
+        await subscription('channel', bufferMessage);
+
+        expect(callback).toHaveBeenCalledWith({
+          err: undefined,
+          response: responseMessage.response,
+        });
+      });
+    });
   });
   describe('close', () => {
     let endSpy: ReturnType<typeof vi.fn>;
---

5	Quantos commits foram feitos nos últimos 90 dias?
- comando utilizado: 
eliab@ELIABS MINGW64 /tmp/nest (master)
$ git rev-list --count --since="90 days ago" --all
- resposta ao comando:
707
