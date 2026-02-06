from telethon import TelegramClient, events

# إعدادات الحساب الشخصي (عشان تتصرف كأنك مستخدم حقيقي)
api_id = 1212216          # حط الـ ID بتاعك هنا
api_hash = '982137ef552883499516fcc2868bfefa'    # حط الـ Hash بتاعك هنا
# اسم الجلسة (ممكن تسميه أي حاجة)
session_name = 'movie_hunter'

# بيانات القنوات والبوتات
SOURCE_CHANNEL = '@CCDBot3' # القناة اللي بتنشر البوستر والرابط
TARGET_CHANNEL = '@CC_3300'     # قناتك اللي هتنشر فيها
OTHER_BOT = '@ccwebot'       # معرف البوت اللي فيه الأفلام

client = TelegramClient(session_name, api_id, api_hash)

@client.on(events.NewMessage(chats=SOURCE_CHANNEL))
async def handler(event):
    # 1. البحث عن رابط البوت في المنشور الجديد
    if OTHER_BOT in event.text:
        print("🔍 لقيت فيلم جديد! جاري الطلب من البوت...")

        # 2. نفتح محادثة مع البوت التاني ونبعت له /start أو الرابط اللي جه
        async with client.conversation(OTHER_BOT) as conv:
            await conv.send_message('/start') # أو تبعت رابط الفيلم اللي في المنشور
            
            # 3. استلام الرد (اللي المفروض يكون فيديو الفيلم)
            response = await conv.get_response()
            
            if response.video:
                print("🎥 استلمت الفيلم بنجاح.. جاري تعديل الوصف والنشر.")
                
                # 4. تغيير الوصف (Caption) ونشره في قناتك
                new_caption = f"🍿 فيلم جديد متاح الآن على بوتنا!\n\nللمشاهدة: @MyNewBot"
                await client.send_file(TARGET_CHANNEL, response.video, caption=new_caption)
                print("✅ تم النشر في قناتك بنجاح!")

print("🚀 السكربت شغال وبيراقب القناة المصدر...")
client.start()
client.run_until_disconnected()
