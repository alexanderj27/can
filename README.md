package frc.robot;

import edu.wpi.first.wpilibj.TimedRobot;
import edu.wpi.first.wpilibj.Joystick;
import edu.wpi.first.wpilibj.drive.DifferentialDrive;

// REV SparkMax imports
import com.revrobotics.spark.SparkMax;
import com.revrobotics.spark.SparkLowLevel.MotorType;

public class Robot extends TimedRobot {

  private SparkMax m_leftMotor;
  private SparkMax m_rightMotor;
  

  private DifferentialDrive m_drive;

  private Joystick m_stick;

  @Override
  public void robotInit() {
    // SparkMax on CAN IDs 1 & 2
    m_leftMotor = new SparkMax(2, MotorType.kBrushed);
    m_rightMotor = new SparkMax(4, MotorType.kBrushed);
   

    // Invert right side (depends on your robot's wiring)
    m_rightMotor.setInverted(true);

    // DifferentialDrive (REV SparkMax supports "set" directly)
    m_drive = new DifferentialDrive(m_leftMotor, m_rightMotor);

    m_stick = new Joystick(0);
  }

  @Override
  public void teleopPeriodic() {
    // Tank drive with one joystick:
    // pushing up drives forward, down drives reverse
    double forward = -m_stick.getY();
    double turn = m_stick.getX();

    // Arcade drive instead of tank (left Y, right X)
    m_drive.arcadeDrive(forward, turn);
  }
}
