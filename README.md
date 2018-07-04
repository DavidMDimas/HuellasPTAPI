# PTAPI Connection

//Please don't remove or modify this Java Class

#FingerprintActivity Java Class
 	private static final String CLOSE_FP_INTENT = "com.taztag.fingerprintservice.CLOSE_FINGERPRINT_EVENT";
    private static final String FP_SERVICE = "FingerprintService";
	private static final String FP_SERVICE_PKG = "com.taztag.fingerprintservice";
	private static final String OPEN_FP_INTENT = "com.taztag.fingerprintservice.OPEN_FINGERPRINT_EVENT";
#IFingerprintService Java Class
	private static final String DESCRIPTOR = "com.taztag.fingerprintservice.IFingerprintService";
	
#put the same package in all the project:
		package com.taztag.fingerprintservice;
        package com.authentec.java.ptapi.samples.basicsample;
        package com.upek.android.ptapi;
        //u would change this package and u could rename manually, but is no necessary
		
#FingerprintConnection Java Class
	//Driver conection to port /dev/ttyHS1 
	private static final String TAG = FingerprintConnection.class.getName();
    private static final String[] mDSNUsb = new String[]{"usb,timeout=500", "wbf,timeout=500"};
    private static final int miRunningOnRealHardware = 1;
    private static final String[] msDSNSerial = new String[]{"port=/dev/ttyHS1,initspeed=2500000,speed=2500000"};
    private static String mydsn = "";
    private PtConnectionAdvancedI mConn = null;
    private PtGlobal mPtGlobal = null;
    private PtInfo mSensorInfo = null;
    private String msNvmPath = null;

#PTAPI Buttons
    setEnrollButtonListener(R.id.ButtonLeftThumb,  FingerId.LEFT_THUMB);
    setEnrollButtonListener(R.id.ButtonLeftIndex,  FingerId.LEFT_INDEX);
    setEnrollButtonListener(R.id.ButtonLeftMiddle, FingerId.LEFT_MIDDLE);
    setEnrollButtonListener(R.id.ButtonLeftRing,   FingerId.LEFT_RING);
    setEnrollButtonListener(R.id.ButtonLeftLittle, FingerId.LEFT_LITTLE);
    setEnrollButtonListener(R.id.ButtonRightThumb, FingerId.RIGHT_THUMB);
    setEnrollButtonListener(R.id.ButtonRightIndex, FingerId.RIGHT_INDEX);
    setEnrollButtonListener(R.id.ButtonRightMiddle,FingerId.RIGHT_MIDDLE);
    setEnrollButtonListener(R.id.ButtonRightRing,  FingerId.RIGHT_RING);
    setEnrollButtonListener(R.id.ButtonRightLittle,FingerId.RIGHT_LITTLE);
    
#List of finger IDs
    /** No finger matched. */
    public static final int NONE = 0x00000000;
    /** Right thumb finger. */
    public static final int RIGHT_THUMB = 0x00000001;
    /** Right index finger. */
    public static final int RIGHT_INDEX = 0x00000002;
    /** Right middle finger. */
    public static final int RIGHT_MIDDLE = 0x00000003;
    /** Right ring. */
    public static final int RIGHT_RING = 0x00000004;
    /** Right little. */
    public static final int RIGHT_LITTLE = 0x00000005;
    /** Left thumb finger. */
    public static final int LEFT_THUMB = 0x00000006;
    /** Left index finger. */
    public static final int LEFT_INDEX = 0x00000007;
    /** Left middle finger. */
    public static final int LEFT_MIDDLE = 0x00000008;
    /** Left ring finger. */
    public static final int LEFT_RING = 0x00000009;
    /** Left little finger. */
    public static final int LEFT_LITTLE = 0x0000000a;

#String representations of finger names
   NAMES[] = {
        "None", "Right Thumb", "Right Index", "Right Middle", "Right Ring", "Right Little",
                "Left Thumb",  "Left Index",  "Left Middle",  "Left Ring",  "Left Little"
    };
    
#PtHelper Java Class (Create message for given GUI callback message)
// Generic GUI messages:            
        case PtConstants.PT_GUIMSG_PUT_FINGER:
        case PtConstants.PT_GUIMSG_PUT_FINGER2:
        case PtConstants.PT_GUIMSG_PUT_FINGER3:
        case PtConstants.PT_GUIMSG_PUT_FINGER4:
        case PtConstants.PT_GUIMSG_PUT_FINGER5:
            s = "Put Finger";
            break;
        case PtConstants.PT_GUIMSG_KEEP_FINGER:
            s = "Keep Finger";
            break;
        case PtConstants.PT_GUIMSG_REMOVE_FINGER:
            s = "Lift Finger";
            break;
        case PtConstants.PT_GUIMSG_BAD_QUALITY:
        case PtConstants.PT_GUIMSG_TOO_STRANGE:
            s = "Bad Quality";
            break;
        case PtConstants.PT_GUIMSG_TOO_LEFT:
            s = "Too Left";
            break;
        case PtConstants.PT_GUIMSG_TOO_RIGHT:
            s = "Too Right";
            break;
        case PtConstants.PT_GUIMSG_TOO_LIGHT:
            s = "Too Light";
            break;
        case PtConstants.PT_GUIMSG_TOO_DRY:
            s = "Too Dry";
            break;
        case PtConstants.PT_GUIMSG_TOO_SMALL:
            s = "Too Small";
            break;
        case PtConstants.PT_GUIMSG_TOO_SHORT:
            s = "Too Short";
            break;
        case PtConstants.PT_GUIMSG_TOO_HIGH:
            s = "Too High";
            break;
        case PtConstants.PT_GUIMSG_TOO_LOW: 
            s = "Too Low";
            break;
        case PtConstants.PT_GUIMSG_TOO_FAST:
            s = "Too Fast";
            break;
        case PtConstants.PT_GUIMSG_TOO_SKEWED:  
            s = "Too Skewed";
            break;
        case PtConstants.PT_GUIMSG_TOO_DARK:  
            s = "Too Dark";
            break;
        case PtConstants.PT_GUIMSG_BACKWARD_MOVEMENT:  
            s = "Backward movement";
            break;
        case PtConstants.PT_GUIMSG_JOINT_DETECTED:  
            s = "Joint Detectected";
            break;
        case PtConstants.PT_GUIMSG_CENTER_AND_PRESS_HARDER:  
            s = "Press Center and Harder";
            break;
        case PtConstants.PT_GUIMSG_PROCESSING_IMAGE:  
            s = "Processing Image";
            break;
        // Enrollment specific:
        case PtConstants.PT_GUIMSG_NO_MATCH:
            s = "Template extracted from last swipe doesn't match previous one";
            break;
        case PtConstants.PT_GUIMSG_ENROLL_PROGRESS:
            s = "Enrollment progress";
