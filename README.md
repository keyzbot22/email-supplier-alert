import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

def send_supplier_email(product_name, qty, supplier_email):
    from_email = "keys.bots@auramarkett.com"
    password = "Moneyman3$"  # or use os.environ.get("ZOHO_APP_PASSWORD")

    msg = MIMEMultipart()
    msg['From'] = from_email
    msg['To'] = supplier_email
    msg['Subject'] = f"Restock Needed: {product_name}"

    body = f"""
    Product: {product_name}
    Quantity Needed: {qty}
    """
    msg.attach(MIMEText(body, 'plain'))

    try:
        server = smtplib.SMTP_SSL('smtp.zoho.com', 465)
        server.login(from_email, password)
        server.sendmail(from_email, supplier_email, msg.as_string())
        print("✅ Email sent successfully!")
    except Exception as e:
        print(f"❌ Error sending email: {e}")
    finally:
        server.quit()

# Test the function
send_supplier_email("Sea Moss Capsules", 50, "supplier@example.com")
