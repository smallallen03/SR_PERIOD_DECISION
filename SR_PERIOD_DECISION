
void SR_PERIOD_DECISION() 
{
    IN  LR int SR_PD, SR_PERIOD ;
    IN  LR int SR_PERIOD_PTCL,SR_PERIOD_WMAC;
    IN  LR int SRG_COUNTER,non_SRG_COUNTER;


	if(SRG_COUNTER != 0)
	{
		// SRG protected case or SRG ReCCA case
		// detect new packet 
		switch (NewOBSSpacket):
		case "SRG SR PASS": // Case 5
			SR_PERIOD_PTCL not update;
			SR_PERIOD_WMAC not update;
			SR_PD not update;
			SRG_COUNTER not update;
		case "SRG SR FAIL": // Case 6
			SR_PERIOD_PTCL = LOW;
			SR_PERIOD_WMAC not update;			
			SR_PD = 0;		
			SRG_COUNTER not update;
		case "non-SRG SR PASS": // Case 7
			SR_PERIOD_PTCL = HIGH(non_SRG_OBSS_TXTIME);
			SR_PERIOD_WMAC = HIGH(non_SRG_OBSS_TXTIME);
			SR_PD = SR_PD(non_SRG_PPDU);
			SRG_COUNTER = 0;
			non_SRG_COUNTER = non_SRG_OBSS_TXTIME;
		case "non-SRG SR FAIL":  // Case 8
			SR_PERIOD_PTCL = LOW;
			SR_PERIOD_WMAC not update;			
			SR_PD = 0;						
			SRG_COUNTER not update;
	}else
	{
		if(non_SRG_COUNTER != 0)
		{
			// ReCCA case, 
			// Reset all signal
			SR_PERIOD_PTCL = LOW;
			SR_PERIOD_WMAC not update;	
			SR_PD = 0;
			non_SRG_COUNTER not update;
				
			switch (NewOBSSpacket):
			case "SRG SR PASS":  // Case 9
				SR_PERIOD_PTCL = HIGH(SRG_OBSS_DURATION);
				SR_PERIOD_WMAC = HIGH(SRG_OBSS_DURATION);
				SR_PD = SR_PD(SRG_PPDU);
				SRG_COUNTER = SRG_OBSS_DURATION;
				non_SRG_COUNTER = 0;				
			case "SRG SR FAIL": // Case 10
				// Do-nothing		
			case "non-SRG SR PASS": // Case 11
				SR_PERIOD_PTCL = HIGH(non_SRG_OBSS_TXTIME);
				SR_PERIOD_WMAC = HIGH(non_SRG_OBSS_TXTIME);
				SR_PD = SR_PD(non_SRG_PPDU);
				non_SRG_COUNTER = non_SRG_OBSS_TXTIME;
			case "non-SRG SR FAIL": // Case 12
				// Do-nothing
		}else {
			// idle state 
			switch (NewOBSSpacket):
			case "SRG SR PASS": // Case 1
				SR_PERIOD_PTCL = HIGH(SRG_OBSS_DURATION);
				SR_PERIOD_WMAC = HIGH(SRG_OBSS_DURATION);
				SR_PD = SR_PD(SRG_PPDU);
				SRG_COUNTER = SRG_OBSS_DURATION;
			case "SRG SR FAIL": // Case 2
				SR_PERIOD_PTCL = LOW;
				SR_PERIOD_WMAC = LOW;	
				SR_PD = 0;		
			case "non-SRG SR PASS": // Case 3
				SR_PERIOD_PTCL = HIGH(non_SRG_OBSS_TXTIME);
				SR_PERIOD_WMAC = HIGH(non_SRG_OBSS_TXTIME);
				SR_PD = SR_PD(non_SRG_PPDU);
				non_SRG_COUNTER = non_SRG_OBSS_TXTIME;
			case "non-SRG SR FAIL": // Case 4
				SR_PERIOD_PTCL = LOW;
				SR_PERIOD_WMAC = LOW;	
				SR_PD = 0;		
		}
	}
	
	
}
